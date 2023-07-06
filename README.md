# Disclaimer

**The purpose of this repository is to provide clear instructions and guidelines for Daml learners to pass the Daml Fundamentals certification via their capstone project. Please bear in mind that any code within is provided for illustrative purposes only, and as such may not be production quality and/or may not fit your use-cases. You may use the contents of this repository in parts or in whole according to the BSD0 license:**

> Copyright © 2023 Digital Asset (Switzerland) GmbH and/or its affiliates
>
> Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted.
>
> THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

# Daml Fundamentals Certificate Sample App

#### 1. Description

    The following project is done as a part of the Daml Fundamentals certification at Digital Asset.

#### 2. Overview

    Time Tracker is a time tracking app that makes it possible for a user to track time they have spent on various tasks belonging to different projects. 

    Minimal solution 

    ● Daml model that implements, creation, update and deletion of the representation of time
    spent. Required data to be stored:
      ○ Description
      ○ Start (date)time
      ○ End (date)time
      ○ A project identifier to allow higher level organization.

    ● A Daml script that can be used to initialize the ledger with at least one user and a few
    sample records.

    ● A Daml script that does some testing of the templates.

    ● Use the Navigator to show how the template can be used.
    
    Additional Daml Code
    ● A Daml contract that can be used to store a summary of the times (all time logged),
    and write scripts that can produce these for a day, a week, a month, a year, a project and
    to date.



#### 3. Compiling & Testing
##### 3.1. Sandbox

    - Navigate to the project folder using your command line and simply run the command `daml start`. 
    It fires up the Sandbox and Navigator for the project. The Navigator will launch in your OS' default browser at port http://localhost:7500/



#### 4. Approach & Workflow

    - Records data type (https://docs.daml.com/daml/intro/3_Data.html#records) is used to create tasks and projects. 
    The record Task has: 
        -- description : Text,
        -- startDate : Time,
        -- endDate : Time and,
        -- projectIdentifier : Text
        -- status : Text

    The record ProjectInfo has:
        -- projectName : Text,
        -- projectDescription : Time,
        -- priority : Text
    
    - The implementation of tasks & project can be found in TaskSetup.daml. The choice to put it in a separate file is to enhance readability.

    - Main.daml contains two templates that creates our contract.
    - ModularTest.daml contains modular testing scripts to test happy and unhappy scenarios.

     The template TimeTracker in Main.daml takes arguments:
    -- owner : Party
    -- myTasks : [Task]
    -- observer : Party
    
    and has choices:
    -- AddTask,
    -- UpdateTask,
    -- RemoveTask,
    -- GetTaskByStatus and,
    -- GetTaskByDueDate

     The template Project in Main.daml takes arguments:
    -- projectInfo : [ProjectInfo]
    -- projectLead : Party
    
    and has choices:
    -- AddProj,
    -- GetProjectsbyPriority
   


#### 5 Extended Functionalities

     - GetTaskByStatus and GetTaskByDueDate are extended functionalities that allow retrieving tasks based on status and due date.

    - GetTaskByStatus:
         - Tasks have a text field called status that can be "To do", "Doing", "Pending" and so on.
         - GetTaskByStatus takes a text input and searches the myTasks list to find Tasks that have a matching status.
         - When invoked, the choice will populate the tasksByStatus list that is initialised when contract is created. tasksByStatus is an Optional parameter
    
    - GetTaskByDueDate takes in a Date input and searches myTasks to find Tasks that have that endDate. 
         - This functionality allows for better time management and easy retrieval of time-sensitive tasks.
         - When invoked, the choice will populate the tasksByDueDate list that is initialised when contract is created. tasksByDueDate is an Optional parameter
    
    - The contract also allows having an observer that can view the contract. This enables the contract owner to 
        give access to the contract data to a 3rd party. Furthermore, the contract code in Main.daml can be 
        modified to allow more than 1 contract owners where all owners have the capacity to exercise all the 
        choices allowed in the contract. This allows collaboration on the contract.

#### 6. Challenges Encountered

    Most notable challenge encountered during development was that the contract not showing up in the Navigator.
  
    The Daml discussion forums were helpful in resolving the issue.
    https://discuss.daml.com/t/navigator-not-showing-contracts/5284



