# CI Workflow with Selenium IDE Tests
### This is a test project for Front-End Test Automation July 2024 Course @ SoftUni

[![C#](https://img.shields.io/badge/Made%20with-C%23-239120.svg)](https://learn.microsoft.com/en-us/dotnet/csharp/)
[![.NET](https://img.shields.io/badge/.NET-5C2D91.svg)](https://dotnet.microsoft.com/)
[![Selenium](https://img.shields.io/badge/tested%20with-Selenium-43B02A.svg)](https://www.selenium.dev/)
[![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-2088FF.svg)](https://github.com/features/actions)

## Selenium IDE

### Step 1: Run the App Locally
Create a CI workflow with GitHub Actions to run the tests automatically.

1. Open Visual Studio and navigate to the Tools menu.
2. Select NuGet Package Manager and then Package Manager Console.
3. Build the application using the following command:
    ```bash
    dotnet build
    ```
4. Ensure the build was successful and run the tests using:
    ```bash
    dotnet test
    ```

### Step 2: Create a GitHub Repo
1. Upload the solution to GitHub.
2. Initialize a repository in your project directory, add the code to the repo, commit, and push:
    ```bash
    git init
    git add .
    git commit -m "Initial commit"
    git remote add origin https://github.com/{name-of-your-repository}
    git push -u origin main
    ```
### Step 3: Add Changes to Test Files
1. Modify the `SetUp()` method of the project to run Chrome in a headless mode within the CI environment.
2. Commit and push the changes:
    ```bash
    git commit -am "Update SetUp method for headless Chrome"
    git push
    ```

### Step 4: Create and Run Workflow
1. Create a GitHub Actions CI workflow:
    - In the root directory of the repository, create a new folder `.github` and inside it create another one called `workflows`.
    - Inside the `workflows` folder, create a YAML file for the workflow definition.
2. Define the workflow file with the following steps:
    - **Checkout code**:
      ```yaml
      - name: Checkout code
        uses: actions/checkout@v2
      ```
    - **Set up .NET Core**:
      ```yaml
      - name: Set up .NET Core
        uses: actions/setup-dotnet@v1
        with:
          dotnet-version: '3.1.x'
      ```
    - **Install Chrome**:
      ```yaml
      - name: Install Chrome
        run: |
          sudo apt-get update
          sudo apt-get install -y google-chrome-stable
      ```
    - **Install dependencies**:
      ```yaml
      - name: Install dependencies
        run: dotnet restore
      ```
    - **Build the solution**:
      ```yaml
      - name: Build the solution
        run: dotnet build --no-restore
      ```
    - **Run the test project**:
      ```yaml
      - name: Run the test project
        env:
          CHROMEWEBDRIVER: /usr/bin/google-chrome
        run: dotnet test --verbosity normal
      ```
3. Commit the workflow file and push the changes to the main branch:
    ```bash
    git add .
    git commit -m "Add CI workflow"
    git push
    ```
4. Ensure the workflow runs successfully.

## Contributing
Contributions are welcome! If you have any improvements or bug fixes, feel free to open a pull request.

## License
This project is licensed under the [MIT License](LICENSE). See the [LICENSE](LICENSE) file for details.

## Contact
For any questions or suggestions, please open an issue in the repository.

---
### Happy Testing! 🚀
