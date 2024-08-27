# Deployer for Azure Data Studio

The Deployer extension for Azure Data Studio streamlines the deployment of `.sql` files, allowing users to execute them in sequence against a selected connection. This eliminates the need for manual file execution.

## Table of Contents

- [Installation](#installation)
- [Features](#features)
  - [Run SQL Files](#run-sql-files)
  - [Select From Table](#select-from-table)
  - [Compare to Current Procedure](#compare-to-current-procedure)
  - [View Procedure Definition](#view-procedure-definition)
  - [Set OpenAI API Key](#set-openai-api-key)
- [License](#license)

## Installation

Currently, installation is only available by manually installing the VSIX package in Azure Data Studio.

## Features

### Run SQL Files

1. Open the command pallet (`CMD + p`) and select `Deployer: Run SQL Files`.
2. Select the files, in order, that you want to execute.
   - Alternatively, select one or more folders containing `.sql` files.
3. Select a connection.
4. The scripts will begin executing.

**What does it do?**

- Executes each selected `.sql` file in sequence.
- If folders are selected, files within them are executed in alphanumeric order.
- After execution, a report summary is available showing the execution status and any errors encountered.

### Select From Table

1. Select a table name in the editor.
2. Open the command pallet (`CMD + p`) and select `Deployer: Select From Table`.
   - Or right-click the selected table in the editor and choose `Deployer: Select From Table` from the context menu.
3. Select a connection.
4. A new editor will open with a `SELECT` statement for the table.

**What does it do?**

- By default, the top 1000 records are selected.
  - Customize this in Settings: `Deployer: Custom Top Select`.
- Add a custom `ORDER BY` clause in Settings: `Deployer: Custom Select Post Statement`, e.g., `ORDER BY 1 DESC`.

### Compare to Current Procedure

_It is recommended to add your OpenAI API key before using this command (see [Set OpenAI API Key](#set-openai-api-key) below)._

1. Open the command pallet (`CMD + p`) and select `Deployer: Compare to Current Procedure`.
2. Select the file containing the stored procedure you want to compare.
3. Select the connection to pull the current procedure from.
4. A diff view will open, showing the currently deployed stored procedure (left) and the selected file (right).

**What does it do?**

- If the OpenAI API Key is set (recommended), the file is sent to OpenAI servers to identify the stored procedure name using AI.
  - This is more effective than using regex.
- Without the API key, Deployer uses regex to find the stored procedure name after the `ALTER` or `CREATE` keyword.
- Once identified, the current procedure version is pulled from the server for comparison.

### View Procedure Definition

1. Select a procedure name in the editor.
2. Open the command pallet (`CMD + p`) and select `Deployer: View Procedure Definition`.
   - Or right-click the selected procuedre in the editor and choose `Deployer: View Procedure Definition` from the context menu.
3. Select the connection to pull the current procedure from.
4. The procedure will be displayed in a new editor

**What does it do?**

- A SQL command is run for the selection that pulls the procedure definition from the selected connection

### Optimize SQL - BETA

_Optimize SQL requires OpenAI API Key_

1. Open the command pallet (`CMD + p`) and select `Deployer: Optimize SQL`.
2. Select the file to optimize
3. A diff will appear with the current and optimized SQL

**What does it do?**

- The file is sent to OpenAI servers with a request to optimize it
- This feature is in BETA and will be improved in future releases

### Set OpenAI API Key

1. Open the command pallet (`CMD + p`) and select `Deployer: Set OpenAI API Key`.
2. Enter your OpenAI API key.

**What does it do?**

- The API key enhances results for commands like `Compare to Current Procedure` and is required for the `Optimize SQL` command.
- The file or selection may be transmitted to OpenAI's servers.

## License

All rights reserved.

