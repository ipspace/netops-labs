# Logging and Testing

In this assignment, you’ll add two testing features to the [project you created in the previous assignment](EX-Create_Service_Data_Model.md):

-   Logging of configuration change results,
-   Unit tests of a single component.

Optional components:

-   Automate unit testing;
-   Validate input data.

## Logging

Add tasks in your playbooks that will log results returned by every interaction with the networking devices (for example, results returned by every **ios\_config** or **ios\_command** task).

Make logging conditional – the results should be logged only when an Ansible variable is set.

**Optional:** Assign a unique ID (example: timestamp) to every playbook run and store logging data for each playbook run in a dedicated subdirectory. This will allow you to examine potential playbook failures even when someone has rerun the playbooks.

## Unit Testing

-   Choose a single component of your project (generating device configurations, transforming the data model…).
-   Create numerous test scenarios with valid and invalid input data.

!!! Tip
    The easiest way to create test scenarios for a component is to store Ansible facts into a YAML or JSON file just before that component is executed in your playbook and then create multiple variants of the input data.

-   Create a test harness for your component. It can be as easy as "read variables for the test scenario, execute the component, save the results."
-   Test your component and verify it returns the expected results under all input conditions.

## Automate Unit Testing

-   Create expected results for all unit tests you created in the previous step. Expected results might be a dump of Ansible variables or a text file with well-known content (for example, device configuration)
-   Create a playbook (or a **bash** script) that will automatically execute all unit tests for your component and compare actual results with expected results

**Hints:**

-   Use **yamllint** to verify your YAML data is well-formatted
-   Use **diff** called with **shell** module to compare text files
-   Use **jq** to [compare JSON documents](http://stackoverflow.com/questions/31930041/using-jq-or-alternative-command-line-tools-to-diff-json-files).

## Validate Input Data

Use [test-driven development approach](https://en.wikipedia.org/wiki/Test-driven_development) in this step:

-   Identify all potential errors in your input data.
-   Create unit tests for the data validation component – variants of input data with one or more errors. Start by introducing a single error in every unit test.
-   Create a test harness for the data validation component and a playbook or **bash** script that automates the unit tests.

!!! Tip
    My test harness is a full-blown Ansible playbook, and as I couldn’t get it to work from within another Ansible playbook (using the **shell** module), I created a **bash** script to automate the unit tests.

After creating the environment:

-   Add code that will detect one of the potential input errors.
-   Execute unit tests to verify that your code detects the error.
-   Repeat as long as feasible. Some errors (for example, duplicate composite keys) are notoriously hard to detect without writing a Python plug-in.

## Useful Links

Explore the [Logging](https://github.com/ipspace/VLAN-service/tree/Logging) and [Pre-deploy check](https://github.com/ipspace/VLAN-service/tree/VLAN_PreDeploy_Check) branches of the [VLAN services project](https://github.com/ipspace/VLAN-service/).
