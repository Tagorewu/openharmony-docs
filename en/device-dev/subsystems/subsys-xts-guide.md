# XTS Test Case Development

## Introduction

The X test suite (XTS) subsystem contains a set of OpenHarmony compatibility test suites, including the currently supported application compatibility test suite (ACTS) and the device compatibility test suite (DCTS) that will be supported in the future.

This subsystem contains the ACTS and **tools** software package.

-   The **acts** directory stores the source code and configuration files of ACTS test cases. The ACTS helps device vendors detect the software incompatibility as early as possible and ensures that the software is compatible to OpenHarmony during the entire development process.
-   The **tools** software package stores the test case development framework related to **acts**.

## System Types

OpenHarmony supports the following systems:

-   Mini system

    A mini system runs on a device that comes with memory greater than or equal to 128 KiB and MCU such as ARM Cortex-M and 32-bit RISC-V. It provides multiple lightweight network protocols and graphics frameworks, and a wide range of read/write components for the IoT bus. Typical products include connection modules, sensors, and wearables for smart home.

-   Small system

    A small system runs on a device that comes with memory greater than or equal to 1 MiB and application processors such as ARM Cortex-A. It provides higher security capabilities, standard graphics frameworks, and video encoding and decoding capabilities. Typical products include smart home IP cameras, electronic cat eyes, and routers, and event data recorders (EDRs) for smart travel.

-   Standard system

    A standard system runs on a device that comes with memory greater than or equal to 128 MiB and application processors such as ARM Cortex-A. It provides a complete application framework supporting the enhanced interaction, 3D GPU, hardware composer, diverse components, and rich animations. This system applies to high-end refrigerator displays.


## Directory Structure

```
/test/xts
├── acts                 # Test code
│   └── subsystem        # Source code of subsystem test cases for the standard system
│   └── subsystem_lite   # Source code of subsystems test cases for mini and small systems
│   └── BUILD.gn         # Build configuration of test cases for the standard system
│   └── build_lite       # Build configuration of test cases for the mini and small systems.
│       └── BUILD.gn     # Build configuration of test cases for mini and small systems
└── tools                # Test tool code
```

## Constraints

Test cases for the mini system must be developed in C, and those for the small system must be developed in C++.

## Usage Guidelines

**Table  1** Test case levels

| Level | Definition | Scope |
| ----- | ----------- | ------- |
| Level0 | Smoke | Verifies basic functionalities of key features and basic DFX attributes with the most common input. The pass result indicates that the features are runnable. |
| Level1 | Basic | Verifies basic functionalities of key features and basic DFX attributes with common input. The pass result indicates that the features are testable. |
| Level2 | Major | Verifies basic functionalities of key features and basic DFX attributes with common input and errors. The pass result indicates that the features are functional and ready for beta testing. |
| Level3 | Regular | Verifies functionalities of all key features, and all DFX attributes with common and uncommon input combinations or normal and abnormal preset conditions. |
| Level4 | Rare | Verifies functionalities of key features under extremely abnormal presets and uncommon input combinations. |


**Table  2** Test case granularities

| Test Scale | Test Objects | Test Environment |
| ----- | ----------- | ------- |
| LargeTest | Service functionalities, all-scenario features, and mechanical power environment (MPE) and scenario-level DFX | Devices close to real devices. |
| MediumTest | Modules, subsystem functionalities after module integration, and DFX | Single device that is actually used. You can perform message simulation, but do not mock functions. |
| SmallTest | Modules, classes, and functions | Local PC. Use a large number of mocks to replace dependencies with other modules. |

**Table  3** Test types

| Type | Definition |
| ----------- | ------- |
| Function | Tests the correctness of both service and platform functionalities provided by the tested object for end users or developers. |
| Performance | Tests the processing capability of the tested object under specific preset conditions and load models. The processing capability is measured by the service volume that can be processed in a unit time, for example, call per second, frame per second, or event processing volume per second. |
| Power | Tests the power consumption of the tested object in a certain period of time under specific preset conditions and load models. |
| Reliability | Tests the service performance of the tested object under common and uncommon input conditions, or specified service volume pressure and long-term continuous running pressure. The test covers stability, pressure handling, fault injection, and Monkey test times. |
| Security | Tests the capability of defending against security threats, including but not limited to unauthorized access, use, disclosure, damage, modification, and destruction, to ensure information confidentiality, integrity, and availability.<br/>Tests the privacy protection capability to ensure that the collection, use, retention, disclosure, and disposal of users' private data comply with laws and regulations.<br/> Tests the compliance with various security specifications, such as security design, security requirements, and security certification of the Ministry of Industry and Information Technology (MIIT). |
| Global | Tests the internationalized data and localization capabilities of the tested object, including multi-language display, various input/output habits, time formats, and regional features, such as currency, time, and culture taboos. |
| Compatibility | Tests backward compatibility of an application with its own data, the forward and backward compatibility with the system, and the compatibility with different user data, such as audio file content of the player and smart SMS messages.<br/>Tests system backward compatibility with its own data and the compatibility of common applications in the ecosystem.<br/>Tests software compatibility with related hardware. |
| User | Tests user experience of the object in real user scenarios. All conclusions and comments should come from the users, which are all subjective evaluation in this case. |
| Standard  | Tests the compliance with industry and company-specific standards, protocols, and specifications. The standards here do not include any security standards that should be classified into the security test. |
| Safety | Tests the safety property of the tested object to avoid possible hazards to personal safety, health, and the object itself. |
| Resilience | Tests the resilience property of the tested object to ensure that it can withstand and maintain the defined running status (including downgrading) when being attacked, and recover from and adapt defense to the attacks to approach mission assurance. |

## Test Case Development Guidelines

The test framework and programming language vary with the system type.

**Table  4** Test frameworks and test case languages for different systems

| System | Test Framework | Language |
| ----- | ----------- | ------- |
| Mini | HCTest | C |
| Small | HCPPTest | C++ |
| Standard | HJSUnit and HCPPTest | JavaScript and C++ |

### Developing Test Cases in C (for the Mini System)

**Developing Test Cases for the Mini System**

HCTest and the C language are used to develop test cases. HCTest is enhanced and adapted based on the open-source test framework Unity.

1. Define the test case directory. The test cases are stored to **test/xts/acts**.

   ```
   ├── acts
   │ └──subsystem_lite
   │ │ └── module_hal
   │ │ │ └── BUILD.gn
   │ │ │ └── src
   │ └──build_lite
   │ │ └── BUILD.gn
   ```
   
2. Write the test case in the **src** directory.

   (1) Include the test framework header file.

   ```
   #include "hctest.h"
   ```

   (2) Use the **LITE_TEST_SUIT** macro to define names of the subsystem, module, and test suite.

   ```
   /**
   * @brief  register a test suite named "IntTestSuite"  
   * @param  test subsystem name  
   * @param  example module name  
   * @param  IntTestSuite test suite name  
   */
   LITE_TEST_SUIT(test, example, IntTestSuite);
   ```
   (3) Define Setup and TearDown.

   ​      Format: Test suite name+Setup, Test suite name+TearDown.

   ​      The Setup and TearDown functions must exist, but function bodies can be empty.    

   (4) Use the **LITE_TEST_CASE** macro to write the test case.

   ​      Three parameters are involved: test suite name, test case name, and test case properties (including type, granularity, and level).
    ```
    LITE_TEST_CASE(IntTestSuite, TestCase001, Function | MediumTest | Level1) 
     {
     // Do something.
      };
    ```
   (5) Use the **RUN_TEST_SUITE** macro to register the test suite.      
    ```
    RUN_TEST_SUITE(IntTestSuite);
    ```
3. Create the configuration file (**BUILD.gn**) of the test module.

   Create a **BUILD.gn** (example) file in each test module directory, and specify the name of the built static library and its dependent header files and libraries. 

   The format is as follows:

   ```
   import("//test/xts/tools/lite/build/suite_lite.gni")
   hctest_suite("ActsDemoTest") {
       suite_name = "acts"
       sources = [
           "src/test_demo.c",
       ]
       include_dirs = [ ]
       cflags = [ "-Wno-error" ]
   }
   ```

4. Add build options to the **BUILD.gn** file in the **acts** directory.

   You need to add the test module to the **test/xts/acts/build\_lite/BUILD.gn** script in the **acts** directory.

   ```
   lite_component("acts") {  
       ...
       if(board_name == "liteos_m") {
           features += [    
               ...
               "//xts/acts/subsystem_lite/module_hal:ActsDemoTest"
           ]    
       }
   }
   ```

5. Run build commands.

   Test suites are built along with the OS version. The ACTS is built together with the debug version.

   >![](../public_sys-resources/icon-note.gif) **NOTE**<br/> The ACTS build middleware is a static library, which will be linked to the image.


### Executing Test Cases in C (for the Mini System)

**Executing Test Cases for the Mini System**

Burn the image into the development board.

**Executing the Test**

1.  Use a serial port tool to log in to the development board and save information about the serial port.
2.  Restart the device and view serial port logs.

**Analyzing the Test Result**

View the serial port logs in the following format:

The log for each test suite starts with "Start to run test suite:"  and ends with "xx Tests xx Failures xx Ignored".

### Developing Test Cases in C++ (for Standard and Small Systems)

**Developing Test Cases for Small-System Devices** (for the standard system, see the **global/i18n_standard directory**.)

The HCPPTest framework, an enhanced version based on the open-source framework Googletest, is used.

1. Define the test case directory. The test cases are stored to **test/xts/acts**.

   ```
   ├── acts
   │ └──subsystem_lite
   │ │ └── module_posix
   │ │ │ └── BUILD.gn
   │ │ │ └── src
   │ └──build_lite
   │ │ └── BUILD.gn
   ```

2. Write the test case in the **src** directory.

   (1) Include the test framework.

      Include **gtest.h**.
	  ```
	  #include "gtest/gtest.h"
	  ```


   (2) Define Setup and TearDown.

      ```
      using namespace std;
      using namespace testing::ext;
      class TestSuite: public testing::Test {
      protected:
      // Preset action of the test suite, which is executed before the first test case
      static void SetUpTestCase(void){
      }
      // Test suite cleanup action, which is executed after the last test case
      static void TearDownTestCase(void){
      }
     // Preset action of the test case
     virtual void SetUp()
     {
     }
     // Cleanup action of the test case
     virtual void TearDown()
     {
      }
      };
     ```


   (3) Use the **HWTEST** or **HWTEST_F** macro to write the test case.

     **HWTEST**: definition of common test cases, including the test suite name, test case name, and case annotation.
    
     **HWTEST_F**: definition of SetUp and TearDown test cases, including the test suite name, test case name, and case annotation.
     
     Three parameters are involved: test suite name, test case name, and test case properties (including type, granularity, and level).
     
     ```
     HWTEST_F(TestSuite, TestCase_0001, Function | MediumTest | Level1) {
     // Do something
     ```

3.  Create a configuration file (**BUILD.gn**) of the test module.

    Create a **BUILD.gn** file in each test module directory, and specify the name of the built static library and its dependent header files and libraries. Each test module is independently built into a **.bin** executable file, which can be directly pushed to the development board for testing.

    Example:
	
	```
	import("//test/xts/tools/lite/build/suite_lite.gni")
	hcpptest_suite("ActsDemoTest") {
	   suite_name = "acts"
       sources = [
           "src/TestDemo.cpp"
       ]
      
       include_dirs = [
           "src",
           ...
       ]
       deps = [
           ...
       ]
       cflags = [ "-Wno-error" ]
	}
	```
    
4.  Add build options to the **BUILD.gn** file in the **acts** directory.

    Add the test module to the **test/xts/acts/build_lite/BUILD.gn** script in the **acts** directory.
	
	```
	lite_component("acts") {  
	...
	else if(board_name == "liteos_a") {
	        features += [
			...
			"//xts/acts/subsystem_lite/module_posix:ActsDemoTest"
			]
		}
	}
	```


5.  Run build commands.

    Test suites are built along with the OS version. The ACTS is built together with the debug version.

    >![](../public_sys-resources/icon-note.gif) **NOTE**
	>
	>The ACTS for the small system is independently built to an executable file (.bin) and archived in the **suites\acts** directory of the build result.


### Executing Test Cases in C++ (for Standard and Small Systems)

**Executing Test Cases for the Small System**

Currently, test cases are shared by the NFS and mounted to the development board for execution.

**Setting Up the Environment**

1. Use a network cable or wireless network to connect the development board to your PC.

2. Configure the IP address, subnet mask, and gateway for the development board. Ensure that the development board and the PC are in the same network segment.

3. Install and register the NFS server on the PC and start the NFS service.

4.  Run the **mount** command for the development board to ensure that the development board can access NFS shared files on the PC.

    Format: **mount** _NFS server IP address_**:/**_NFS shared directory_ **/**_development board directory_ **nfs**

    Example: 

    ```
    mount 192.168.1.10:/nfs /nfs nfs
    ```
    
    

**Executing Test Cases**

Execute **ActsDemoTest.bin** to trigger test case execution, and analyze serial port logs generated after the execution is complete.

### Developing Test Cases in JavaScript (for the Standard System)

The HJSUnit framework is used to support automated test of OpenHarmony apps that are developed using the JavaScript language based on the JS application framework.

**Basic Syntax of Test Cases**

The test cases are developed with the JavaScript language and must meet the programming specifications of the language.

**Table  5** Basic syntax of test cases

| Syntax | Description | Mandatory |
| ------- | ------------- | ------------ |
| beforeAll | Presets a test-suite-level action executed only once before all test cases are executed. You can pass the action function as the only parameter. | No |
| afterAll | Presets a test-suite-level clear action executed only once after all test cases are executed. You can pass the clear function as the only parameter. | No |
| beforeEach | Presets a test-case-level action executed before each test case is executed. The number of execution times is the same as the number of test cases defined by it. You can pass the action function as the only parameter. | No |
| afterEach | Presets a test-case-level clear action executed after each test case is executed. The number of execution times is the same as the number of test cases defined by it. You can pass the clear function as the only parameter. | No |
| describe | Defines a test suite. You can pass two parameters: test suite name and test suite function. The describe statement supports nesting. You can use beforeall, beforeEach, afterEach, and afterAll in each describe statement. | Yes |
| it | Defines a test case. You can pass three parameters: test case name, filter parameter, and test case function. <br>**Filter parameter:** <br/>The value is a 32-bit integer. Setting different bits to 1 means different configurations.<br/> - Setting bit 0 to **1** means bypassing the filter. <br>- Setting bits 0-10 to **1** specifies the test case type, which can be FUNCTION (function test), PERFORMANCE (performance test), POWER (power consumption test), RELIABILITY (reliability test), SECURITY (security compliance test), GLOBAL (integrity test), COMPATIBILITY (compatibility test), USER (user test), STANDARD (standard test), SAFETY (security feature test), and RESILIENCE (resilience test), respectively.<br>- Setting bits 16-18 to **1** specifies the test case scale, which can be SMALL (small-scale test), MEDIUM (medium-scale test), and LARGE (large-scale test), respectively.<br>- Setting bits 24-28 to **1** specifies the test level, which can be LEVEL0 (level-0 test), LEVEL1 (level-1 test), LEVEL2 (level-2 test), LEVEL3 (level-3 test), and LEVEL4 (level-4 test), respectively.<br> | Yes |

Use the standard syntax of Jasmine to write test cases. The ES6 specification is supported.

1.  Define the test case directory. The test cases are stored in the **entry/src/main/js/test** directory.

    ```
	├── BUILD.gn   
	│ └──entry
	│ │ └──src
	│ │ │ └──main
	│ │ │ │ └──js
	│ │ │ │ │ └──default
	│ │ │ │ │ │ └──pages
	│ │ │ │ │ │ │ └──index
	│ │ │ │ │ │ │ │ └──index.js        # Entry file
	│ │ │ │ │ └──test                  # Test code directory  
	│ │ │ └── resources                # HAP resources
	│ │ │ └── config.json              # HAP configuration file
	```


2. Start the JS test framework and load test cases. 

   The following is an example for **index.js**.

   ```
   // Start the JS test framework and load test cases.
    import {Core, ExpectExtend} from 'deccjsunit/index'
    
    export default {
       data: {
   	      title: ""
   	},
       onInit() {
          this.title = this.$t('strings.world');
      },
       onShow() {
          console.info('onShow finish')
          const core = Core.getInstance()
          const expectExtend = new ExpectExtend({
              'id': 'extend'
          })
          core.addService('expect', expectExtend)
          core.init()
          const configService = core.getDefaultService('config')
          configService.setConfig(this)
          require('../../../test/List.test')
          core.execute()
      },
      onReady() {
      },
   }
   ```

   

3. Write a unit test case.

   The following is an example:

   ```
   // Example 1: Use HJSUnit to perform a unit test.
   describe('appInfoTest', function () {    
      it('app_info_test_001', 0, function () {
          var info = app.getInfo()
   	   expect(info.versionName).assertEqual('1.0')
   	   expect(info.versionCode).assertEqual('3')
      })
   }) 
   ```

   


### Packaging Test Cases in JavaScript (for the Standard System)

For details about how to build a HAP, see the JS application development guide of the standard system [Building and Creating HAPs](https://developer.harmonyos.com/en/docs/documentation/doc-guides/build_overview-0000001055075201).

## Performing a Full Build (for the Standard System)

Run the following command:

```
./build.sh suite=acts system_size=standard
```

 


Test case directory: **out/release/suites/acts/testcases**

Test framework and test case directory: **out/release/suites/acts** \(the test suite execution framework is compiled during the build process)


## Executing Test Cases in a Full Build (for Small and Standard Systems)

**Setting Up a Test Environment**

Install Python 3.7 or a later version on a Windows environment and ensure that the Windows environment is properly connected to the test device.

**Test execution directory** \(corresponding to the **out/release/suites/acts** directory generated in the build)

```
├── testcase                       # Directory for storing test suite files
│ └──xxx.hap                       # HAP file executed by the test suite
│ └──xxx.json                      # Execution configuration file of the test suite
├── tools                          # Test framework tool directory
├── run.bat                        # File for starting the test suite on the Windows platform
├── report                         # Directory for storing the test reports
```

**Executing Test Cases**

1.  On the Windows environment, locate the directory in which the test cases are stored \(**out/release/suites/acts**, copied from the Linux server), go to the directory in the Windows command window, and run **acts\\run.bat**.

2.  Enter the command for executing the test case.

    -   Execute all test cases.

      ```
      run acts
      ```
      
      ![](figure/en-us_image_0000001119924146.gif)
      
    -   Execute the test cases of a module \(view specific module information in **\acts\testcases\**).
    
      ```
      run –l ActsSamgrTest
      ```
      
      ![](figure/en-us_image_0000001166643927.jpg)
      
      You can view specific module information in **\acts\testcases\**.
      
      Wait until the test cases are complete.

3.  View the test report.

    Go to **acts\reports**, obtain the current execution record, and open **summary_report.html** to view the test report.
