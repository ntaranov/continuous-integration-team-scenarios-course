## Discuss the changes, add more commits as discussion continues  

### Pull requests

<details><summary>Pull request(PR) is a popular way to discuss, review and document code changes as they occur.</summary>
Pull requests are named after a common way of integrating individual contributions into shared codebase. Normally, a person clones a remote official project repository and works on the code locally. After, he pushes the code into his personal remote repository and asks the official repository's maintainers to <strong>pull</strong> his code into their local repositories where they review and potentially <strong>merge</strong> it. The same concept is known under different names, e.g., "merge request".  
</details>

Actually, you don't have to use pull request feature of GitHub or similar platforms. Teams can use other modes of communication including face-to-face communication, voice calls, or e-mails, but there is a number of reasons to use such forum thread-like pull requests. Here are some of them:
- to organize discussions related to specific changes in code;
- as a place to show feedback on work in progress, from both auto tests and colleagues;
- to formalize code reviews;
- to make it possible to figure out the reasons and considerations behind a given piece of code later. 

<details><summary>You generally open a pull request when you need to discuss something or receive feedback.</summary>
For example, if you work on a feature that might be implemented in a number of ways, you might want to open a pull request even before writing the first line of code to share your ideas and to discuss your plans with the collaborators. If the work is more straightforward, the pull request is opened when something is already done, committed, and can be discussed. In some scenarios, you might open a PR just for the sake of quality assurance: to trigger auto tests or to initiate a code review. Whatever you decide, don't forget to @mention persons whose approval is required in your pull request.
</details>

Usually, you do these things when creating a PR.
- Specify what you suggest to merge where.
- Write a description explaining the purpose of the pull request. You might want to:
  - add anything important that isn't obvious from the code and anything  helpful to understand the context such as relevant #issues and commit numbers;
  - @mention everyone you want to start collaborating with, or you can @mention them in a comment later;
  - ask your colleagues to do or check something specific.

After you open a PR, whatever automated tests scheduled are run on your code. In our case, this is going to be the same test suite as we ran locally, but in a real project, there might be extra tests and checks.

Please, wait until the tests finish running. You can see the status of the tests at the bottom of the PR discussion thread. I'll give further instructions in a comment when the tests are done.

<details><summary>What to do if the comment doesn't appear</summary>

- Wait a couple of minutes;
- Refresh the page;
- Re-launch the checks with GitHub UI under the **Actions** tab.
</details>
