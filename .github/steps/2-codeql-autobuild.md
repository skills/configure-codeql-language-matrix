## Step 2: Have autobuild run only when needed

_Nice work! :tada: You modified your workflow to use a language matrix!_

With the language matrix specified we can see the languages we want to scan. One of those languages is a compiled language, and as such, will not work correctly with how we have the workflow set up. We need to make sure the autobuild step is included _and_ only runs when it is needed.

Autobuild for CodeQL is a feature that automatically attempts to build any compiled languages in your repository. It works by detecting the build system in your repository and executing the appropriate commands to compile the code, enabling CodeQL to analyze the compiled language.

Let's try this out with our existing CodeQL workflow file.

### :keyboard: Activity: Configure the workflow to use autobuild for the `java-kotlin` language

1. Navigate to the `.github/workflows` directory in your repository.
1. Open the `codeql.yml` file.
1. Add the autobuild step to the file in between the `Initialize CodeQL` and `Perform CodeQL Analysis` steps:
    ```yaml
    - name: Autobuild
      uses: github/codeql-action/autobuild@v3
    ```
1. Ensure that your indentation is correct after adding the step.
1. Now we need to make sure that the autobuild step only runs when it is needed. Add to the `Autobuild` step a conditional expression that checks to make sure the language is `java-kotlin`.

<details>
  <summary>Autobuild step after adding conditional</summary>

```yaml
    - if: ${{ contains(matrix.language, 'java-kotlin') }}
      name: Autobuild
      uses: github/codeql-action/autobuild@v3
```

</details>
    
1. Commit the changes directly to the `main` branch.
1. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.
