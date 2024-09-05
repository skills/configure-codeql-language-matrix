## Step 1: Add a language matrix to your CodeQL workflow file

_Welcome to "Configuring a CodeQL language matrix"! :wave:_

## CodeQL language matrices

CodeQL language matrices allow you to configure your CodeQL workflows with a language matrix to simplify your code scanning workflows. This allows you to have a single code scanning workflow that covers all the languages in your repository.

### Importance of using languages matrices with code scanning

1. **Simplicity**: Using a language matrix with CodeQL simplifies your workflow by allowing you to manage multiple languages in a single workflow file. This eliminates the need for separate workflows for each language, making your code scanning process more streamlined and manageable.
2. **Flexibility**: A language matrix provides flexibility, as it allows you to easily add or remove languages from your workflow. This means you can quickly adapt your code scanning process to changes in your project's language usage.
3. **Consistency**: By using a language matrix, you ensure consistent code scanning across all languages used in your project. This helps maintain the quality and security of your codebase, regardless of the language it's written in.

Remember, a well-configured CodeQL setup is key to maintaining a secure and reliable codebase.

### :keyboard: Activity: Configure your `codeql.yml` file to use a language matrix

1. In the `Code` tab, locate the `.github/workflows` folder.
1. In the `codeql.yml` file, above the `steps` section, add the following:
    ```yaml
    strategy:
      fail-fast: false
      matrix:
        language: [ 'go', 'java-kotlin', 'javascript-typescript', 'python' ]
        # CodeQL supports [ 'c-cpp', 'csharp', 'go', 'java-kotlin', 'javascript-typescript', 'python', 'ruby', 'swift' ]
        # Use only 'java-kotlin' to analyze code written in Java, Kotlin, or both
        # Use only 'javascript-typescript' to analyze code written in JavaScript, TypeScript, or both
        # Learn more about CodeQL language support at https://aka.ms/codeql-docs/language-support

    ```
1. Ensure that your indentation is correct after adding the strategy section.
1. Now that you have added the strategy, you need to update CodeQL to actually use the language matrix. Add the following to the CodeQL init action:
    ```yaml
      with:
        languages: ${{ matrix.language }}
    ```
1. Finally, we need to add the language matrix to the CodeQL analyze action. Add the following to the CodeQL analyze action:
    ```yaml
      with:
        category: ${{ matrix.language }}
    ```
1. Commit the changes directly to the `main` branch.
1. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.
