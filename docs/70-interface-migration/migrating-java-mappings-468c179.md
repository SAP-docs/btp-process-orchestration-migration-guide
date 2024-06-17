<!-- loio468c1794f33d40de85638249a5348ff0 -->

# Migrating Java Mappings

Migrate your Java mappings in SAP Process Orchestration to the more efficient Groovy script in Cloud Integration using Groovy script templates.



<a name="loio468c1794f33d40de85638249a5348ff0__section_d4x_vpr_g1c"/>

## Groovy Script vs. Java Mapping

When you transition from SAP Process Orchestration to the Cloud Integration capability within SAP Integration Suite, you can use Groovy scripts instead of Java mappings. Groovy has a few advantages over Java mappings, for example, Groovy scripts have a more concise and expressive syntax, which reduces the amount of code needed for common tasks. Groovy's flexibility and simplicity make it well suited for quick development cycles and easy maintenance, and it seamlessly integrates with Java, which eases the transition for developers familiar with Java. Overall, using Groovy in your Cloud Integration environment leads to more efficient development and easier management of integration processes. For a list of syntax differences between the two programming languages, see [Differences with Java](http://groovy-lang.org/differences.html).

The following table provides an overview of the different functions used in Java mappings and Groovy script.


<table>
<tr>
<th valign="top">

Header Function

</th>
<th valign="top">

Java Mappings \(SAP Process Orchestration\)

</th>
<th valign="top">

Groovy Script \(Cloud Integration\)

</th>
</tr>
<tr>
<td valign="top">

**Message Input and Output Classes** 

</td>
<td valign="top">

-   `AbstractTransformation.getInputPayload`: Get the input payload \(message\) in the Java mapping.

-   `AbstractTransformation.getOutputPayload`: Get the output payload \(message\) in the Java mapping.




</td>
<td valign="top">

Access input and output messages using the `message` object.

For example, use `message.getBody()` to get the input payload and `message.setBody()` to get the output payload.

</td>
</tr>
<tr>
<td valign="top">

**XML Processing** 

</td>
<td valign="top">

Java mappings often involve XML processing. Use classes like `DocumentBuilderFactory`, `DocumentBuilder`, or `Document` for reading, creating, and manipulating XML documents.

</td>
<td valign="top">

Groovy has built-in support for XML processing. To read and create XML documents, use Groovy's XMLSlurper or XMLBuilder classes.

</td>
</tr>
<tr>
<td valign="top">

**Logging and Tracing** 

</td>
<td valign="top">

-   `AbstractTransformation.getTrace().addInfo`: Add informational messages to the mapping log.

-   `AbstractTransformation.getTrace().addWarning`: Add warning messages to the mapping log.

-   `AbstractTransformation.getTrace().addError`: Add error messages to the mapping log.




</td>
<td valign="top">

The message processing log \(MPL\) stores data about the messages processed on a tenant. It also stores information about the individual processing steps for each processed message. For more information on using the MPL in your Groovy script, see [Add Information to the Message Processing Log](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/add-information-to-message-processing-log?locale=en-US&version=Cloud).

</td>
</tr>
<tr>
<td valign="top">

**Exception Handling** 

</td>
<td valign="top">

Java mappings handle exceptions appropriately using try-catch blocks.

Use `AbstractTransformation.getTrace()` to write additional messages on the log console.

</td>
<td valign="top">

Groovy supports try-catch blocks for exception handling. Additionally, you can use the object `CamelExceptionCaught` to retrieve more information about exceptions thrown in your integration flow.

See [Script Example for Exception Handling in HTTP Receiver](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/script-example-for-exception-handling-in-http-receiver?locale=en-US&version=Cloud).

</td>
</tr>
</table>

You can directly migrate small Java mappings to Groovy scripts. For more complex scenarios, you can still reuse some of your existing Java mappings from SAP Process Orchestration in Cloud Integration, but you must use a **Groovy script wrapper**. Also, your Java mapping must use supported functions and methods on Cloud Integration.

In all cases, make sure to retest the Java mappings after the import and adapt them if necessary.

The following use cases found in Java mappings might not be supported using this Groovy wrapper approach in Cloud Integration:

-   Binary attachments \(for example, PDF\)

-   Process Microsoft Office documents \(for example, Word, Excel\)

-   Encryptions and decryptions

-   Java mapping lookups

-   File system operations

-   Message signature using certificate in keystore

-   Dynamic properties and headers




<a name="loio468c1794f33d40de85638249a5348ff0__section_p2y_4zl_g1c"/>

## Using the Groovy Wrapper Script to Invoke the Java Mapping

Before you import the JAR file, confirm how the Java mapping was previously implemented.

If the Java mapping inherits the `AbstractTransformation` class, use the following Groovy script template. You can identify the case based on the declaration statement `public class CopyPDFtoPayload extends AbstractTransformation`.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap; 
import com.sap.aii.mapping.api.*;
/*
In the Import section, insert the class name of your java mapping. If your full class name is “com.custom.company.ReplaceXMLNamespaces”, then the final result is presented below:
*/
import com.custom.company.ReplaceXMLNamespaces;

def Message processData(Message message) {
    //Create a new instance of the Java Mapping using the class name imported previously:
    ReplaceXMLNamespaces javaMapping = new ReplaceXMLNamespaces();
    
    MyTransformationInput  transformationInput  = new MyTransformationInput(message);
    MyTransformationOutput transformationOutput = new MyTransformationOutput();
    
    def result = javaMapping.transform(transformationInput,transformationOutput);
    
    String resultString = new String(transformationOutput.getOutputPayload().getOutputStream().toByteArray());
        
    message.setBody(resultString);
    
    return message;
}

class MyTransformationInput extends TransformationInput {
    
    private MyInputPayload inputPayload;
    
    MyTransformationInput(Message message){
        inputPayload = new MyInputPayload(message);
    }
    
    @Override
    InputPayload getInputPayload() {  
        return inputPayload;   
    }
    
    @Override
    InputHeader getInputHeader() {}

    @Override
    InputParameters getInputParameters() {}

    @Override
    InputAttachments getInputAttachments() {}
 
    @Override
    DynamicConfiguration getDynamicConfiguration() {}
}

class MyInputPayload extends InputPayload {
    private InputStream input;
    
    MyInputPayload(Message message){
        def body = message.getBody(java.lang.String) as String;
        input = new ByteArrayInputStream( body.getBytes( 'UTF-8' ) );
    }
    
    @Override
    InputStream getInputStream() {  
        return input;
    }
}

class MyTransformationOutput extends TransformationOutput {
    
    private MyOutputPayload outputPayload;
    
    MyTransformationOutput(){
        outputPayload = new MyOutputPayload();
    }
    
    @Override
    OutputPayload getOutputPayload() {  
        return outputPayload;   
    }
    
    @Override
    OutputHeader getOutputHeader() {}

    @Override
    OutputParameters getOutputParameters() {}

    @Override
    OutputAttachments getOutputAttachments() {}
 
    @Override
    void copyInputAttachments() {}
}

class MyOutputPayload extends OutputPayload {
    private ByteArrayOutputStream output;
    
    MyOutputPayload(){
        output = new ByteArrayOutputStream();
    }
    
    @Override
    OutputStream getOutputStream() {  
        return output;
    }
}
```

Since the classes `TranformationInput`, `InputPayload`, `TranformationOutput`, and `OutputPayload` are abstract, the objective of this Groovy template is to provide a minimum implementation to support the expected call in the original Java mapping. Enhance the template as you need it.

Alternatively, if the original Java mapping implements the `StreamTransformation` interface, you can use the following Groovy script template. You can identify the case based on the declaration statement `public class MarkantInvoiceSplitMapping extends Object Implements StreamTransformation`.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
/*
In the Import section, insert the class name of your java mapping. If your full class name is “com.custom.company.ReplaceXMLNamespaces”, then the final result is presented below:
*/
import com.custom.company.ReplaceXMLNamespaces;

def Message processData(Message message) {
    def body = message.getBody(java.lang.String) as String;

    //Create a new instance of the Java Mapping using the class name imported previously:
    ReplaceXMLNamespaces javaMapping = new ReplaceXMLNamespaces();
        
    InputStream inputStream = new ByteArrayInputStream( body.getBytes( 'UTF-8' ) );
    
    ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
    
    def result = javaMappingPayloadNamespace.execute(inputStream,outputStream);
    
    String resultString = new String(outputStream.toByteArray());
        
    message.setBody(resultString);
    
    return message;
}
```

The method defined by the `StreamTransformation`, `execute()`, expects to receive an `InputStream` and `OutputStream`. Therefore, you can call it directly.

> ### Caution:  
> The `StreamTransformation` interface is **deprecated**. See [Interface StreamTransformation](https://help.sap.com/doc/2f39047ed6b141cb83658041d2d4e029/7.5.latest/en-US/PI/com/sap/aii/mapping/api/StreamTransformation.html).

To proceed with either approach, complete the following steps:

1.  Import the JAR file into the *Resources* section of the integration flow.

2.  Create a new Groovy script. Copy and paste one of the previous templates.

3.  Edit the copied template: Enter the correct name of the class you want to import and the object you want to instantiate.

4.  Test your integration flow and compare the results between SAP Process Orchestration and Cloud Integration using the same source message.


When you transition Java mappings from SAP Process Orchestration to Cloud Integration, reimplement the Java mapping as a Groovy script to align with SAP's recommended approach. Based on your specific use case, you can employ the Groovy wrapper script to invoke the Java mapping within Cloud Integration.

> ### Note:  
> Alternatively, you can explore using Generative AI for this use case. However, this approach currently differs from the SAP recommendation. If you want to explore Generative AI, make sure you check the disclaimer sections in the blogs [Using Generative AI to Migrate Java Mapping to Cloud Integration - Part 1: The Concept](https://community.sap.com/t5/technology-blogs-by-sap/using-generative-ai-to-migrate-java-mapping-to-cloud-integration-part-1-the/ba-p/13583434) and [Using Generative AI to Migrate Java Mapping to Cloud Integration - Part 2: A Sample](https://community.sap.com/t5/technology-blogs-by-sap/using-generative-ai-to-migrate-java-mapping-to-cloud-integration-part-2-a/ba-p/13583450) beforehand.

