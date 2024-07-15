<!-- loioe3735695d87c421ea0fb862e02c0f668 -->

# Testing the Pipeline

SAP's partners provide regression test tools that you can use to test your integration scenarios and apply the pipeline concept.

The following partner offerings support the pipeline concept in their migration and regression test tools:

-   Learn about **Int4**'s offerings in the blog [SAP Pipeline Concept and B2B TPM Testing](https://community.sap.com/t5/technology-blogs-by-members/sap-pipeline-concept-and-b2b-tpm-testing/ba-p/13691706).

-   Learn about **Figaf**'s offerings in the blog [Testing SAP Pipeline Concept Flows with Figaf](https://community.sap.com/t5/technology-blogs-by-members/testing-sap-pipeline-concept-flows-with-figaf/ba-p/13754121).


Furthermore, the new header **`testMode`** is passed between the sequence of integration flows. Use this `testMode` header to define the processing behavior for scenario tests, for example, when sending the message to a mocked receiver instead of to the actual receiver. See [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc) and [IDoc Sender Adapter](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_tjw_z3f_j1c).

**Related Information**  


[Test Automation](test-automation-4566dd2.md "As part of the testing phase in every migration project, several products on the market help you to create automatic testing scenarios. Test automation reduces risks to critical business processes and lowers the human effort to cover the test tasks of your interfaces.")

