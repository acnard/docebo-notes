##  python setup notes

install VS code, python, and the python extension plus jupyter notebooks

- I installed python using the mac installer from python.org, I also had to install xcode.

nb. to check the presence of python, in the terminal you have to type `python3 --version`
pip is automatically installed when you install python

### install the openai python library

`pip3 install openai` to install the openai library

At this point, in the VS code jupyter notebook the following does not give an error:

```python
import openai
import os
```

### get an api key

go to https://platform.openai.com/api-keys (I logged in with personal gmail account sso) and generate an api key there.

my key: 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

Then this link of code sets your open api key in a variable:

```py
openai.api_key="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"
```

Nb this key was later disabled because I had pushed it to github

## Git setup notes

There is a version of git installed on the mac, probably as a result of installing Xcode when I installed python.

<img src="image-20240315103443018.png" alt="image-20240315103443018" style="zoom:50%;" />

In github I had already created the docebo-notes repo:

nb to create subfolders in the repo use create new file and then append a slash (/) to the filename you specify.

<img src="image-20240315103758209.png" alt="image-20240315103758209" style="zoom:50%;" />

### clone repo to local machine

In *Finder* navigate to the folder where you want to clone the repo, right click it and select **copy**. This will copy the folder path.

<img src="image-20240315104836485.png" alt="image-20240315104836485" style="zoom:50%;" />

Now in Terminal type cd and paste in the path you copied above. 

<img src="image-20240315105010793.png" alt="image-20240315105010793" style="zoom:50%;" />

Now over on githup select Clone and copy the https URL of the repo, and back in terminal use the git cone command.

<img src="image-20240315105207077.png" alt="image-20240315105207077" style="zoom:50%;" />

And you can see that the folder structure you created in the repo is cloned to your local machine:

<img src="image-20240315105335857.png" alt="image-20240315105335857" style="zoom:50%;" />



### try git commands

Now let's try adding some content into the repo: move into it the jupyter notebook files from the prompt engineering course.

Now if we cd into the docebo-notes directory and do a `git status` it tells us about the untracked files. 

<img src="image-20240315105913501.png" alt="image-20240315105913501" style="zoom:50%;" />

We can track them with `git add -A` , after which it tells us about the changes that need to be commited:

<img src="image-20240315110119732.png" alt="image-20240315110119732" style="zoom:50%;" />

### configure name and email

But if we try to do a git commit at this point it complains that it doesn't know who I am. Because we have to do the configuration part:

<img src="image-20240315110655835.png" alt="image-20240315110655835" style="zoom:50%;" />

see also: https://training.github.com/downloads/github-git-cheat-sheet/

Now with these I can do a commit (not sure how to enter the commit message into the terminal though.... hit "esc" and then write :wq to write then quit.

But now if I try to do a git push it tells me I can't use email and password authentication any more, so I would have to set up a token (or something)...

### use VS code

let's try to open the local repo folder in vscode.

Now the source control recognizes that I have committed changes that need to be pushed to the remote. When I tell it to sync (that is , do a push- pull), it asks me to <img src="image-20240315114734700.png" alt="image-20240315114734700" style="zoom:50%;" /> sign in.

#### authentication via GitHub

And the VS code github extension then asks me to authorise:

<img src="image-20240315114838734.png" alt="image-20240315114838734" style="zoom:50%;" />

#### push blocked due to secret

and github asks me for my password:

<img src="image-20240315115030975.png" alt="image-20240315115030975" style="zoom: 33%;" />

But then the push was blocked because the code I'd pushed contained a "secret" (the open api key):

<img src="image-20240315115652366.png" alt="image-20240315115652366" style="zoom:50%;" />

So I removed this part from the file and then I was able to sync from vscode.

#### push was failing with 400 error 

From both VS code and the terminal, I had this error:

"Git: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400"

It was fixed by increasing the buffers size. With the below command, I was able to re-add the mac setup notes to the repo and push all changes to github origin. 

**Large Files or Repository**

- If the repository or changes being pushed are large, increase Git’s buffer size:

  ```
  bash
  
  
  CopyEdit
  git config --global http.postBuffer 524288000
  ```



