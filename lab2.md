**Exercise \#2: Setup a runner and a workflow**

1)  Go back to the repository we created in the previous exercise and
    click on the “settings” tab. Then within the “Code and automation”
    section from the left menu, click on “Actions” \> “runners” and then
    click on the green “New self-hosted runner” button at the top
    right.:

<img src="./images/media/image7.png"
style="width:8.92507in;height:4.99079in" />

2)  Select your Operating System in “Runner image” and your architecture
    (x64/arm)

3)  Follow the steps listed below architecture to download and install
    the runner (Hint: you can copy the commands by clicking on them)

4)  Example for Windows:\
    Open Terminal or Cmd/Powershell **<span class="mark">as
    administrator</span>** and create a folder called “actions-runner”
    in the drive root and open that directory:\
    \
    <img src="./images/media/image8.png"
    style="width:6.03125in;height:3.01042in"
    alt="Text Description automatically generated" />

5)  Download the latest runner package:

<img src="./images/media/image9.png"
style="width:9.23522in;height:2.31128in"
alt="Text Description automatically generated" />

6)  Check the integrity of the downloaded file to make sure its
    legitimate (if it has been compromised it will display the message
    saying “Computed checksum did not match”):\
    <img src="./images/media/image10.png"
    style="width:9.36622in;height:0.83055in" />

7)  Extract the file contents to the current location:\
    <img src="./images/media/image11.png"
    style="width:9.14351in;height:3.98438in"
    alt="Text Description automatically generated" />

8)  Register the runner to your github repository with the first command
    in the “Configure” section. You can leave the default values for
    name, labels and work folder or change them\
    when prompted if you would like to run it as a service select “y”,
    and select the default account to use for the service (NT
    Authority\Network service):\
    <img src="./images/media/image12.png"
    style="width:7.36845in;height:6.99351in"
    alt="Text Description automatically generated" />

9)  Once you have completed the previous step, your runner should appear
    as online/idle within the repository “settings \> actions \>
    runners”\
    \
    <img src="./images/media/image13.png"
    style="width:8.13542in;height:2.41667in" />

10) If it appears as offline, you may need to run the “./run.cmd”
    command\
    \
    <img src="./images/media/image14.png"
    style="width:3.54167in;height:1.05208in"
    alt="Text Description automatically generated" />

11) Now we are ready to test our runner. Click on “Code”, then on the
    “Add file” button and select “Create new file”\
    \
    <img src="./images/media/image15.png"
    style="width:9.07292in;height:2.45833in" />

12) At the top part, type “.github/”, then “workflows/”, and then
    “firstWorkFlow.yml”:\
    \
    <img src="./images/media/image16.png"
    style="width:7.375in;height:2.51042in"
    alt="Graphical user interface, application, website Description automatically generated" />

Add the following code to the file, mind the 2 spaces between each
indent.\
Note: if you set up a self-hosted Linux/macOS runner in the previous
step, you need to <span class="mark">change</span> line 11 (shell: cmd)
to (<span class="mark">shell: bash</span>):\
\
<img src="./images/media/image17.png"
style="width:7.60417in;height:5.59375in"
alt="A screenshot of a computer screen Description automatically generated" />
 
```yaml
name: first workflow

on:
  workflow_dispatch:

jobs:
  firstjob:
    runs-on: self-hosted
    steps:
      - name: firstJob script
        shell: cmd
        run: echo Hello World! This is the first job

  secondjob:
    runs-on: ubuntu-latest
    steps:
      - name: secondJob script
        shell: bash
        run: |
          echo this is the second job
          echo and this is a multi-line script
```


13) Click on the green “Commit changes..” button on the right side,
    leave “Commit directly to the main branch” selected and next click
    on the green “Commit changes” button.\
    \
    <img src="./images/media/image18.png"
    style="width:7.89583in;height:6.5in"
    alt="A screenshot of a computer Description automatically generated" />

14) Click on “Actions”, you should see your workflow listed there:\
    \
    <img src="./images/media/image19.png" style="width:9in;height:5.04167in"
    alt="A screenshot of a computer Description automatically generated" />

15) Next, select your workflow and click on “run workflow”, select
    “main” branch, and click on “run workflow”\
    <img src="./images/media/image20.png" style="width:9in;height:3.82569in"
    alt="A screenshot of a computer Description automatically generated" />

16) After a couple of seconds, the job will be launched, and you can see
    its details by clicking on it:\
    \
    <img src="./images/media/image21.png"
    style="width:8.9933in;height:3.17907in"
    alt="A screenshot of a computer screen Description automatically generated with medium confidence" />

17) Here you can see it is a workflow made up of 2 jobs\
    \
    <img src="./images/media/image22.png"
    style="width:9.02751in;height:5.05143in"
    alt="A screenshot of a computer Description automatically generated with medium confidence" />

18) Upon clicking on each job, you can see the steps within:\
    \
    <img src="./images/media/image23.png"
    style="width:9.08333in;height:4.5in"
    alt="A screenshot of a computer Description automatically generated with medium confidence" />\
    \
    <img src="./images/media/image24.png" style="width:7.45833in;height:4in"
    alt="A screenshot of a computer Description automatically generated with medium confidence" />

19) Now lets go ahead and remove the self-hosted runner.\
    This is especially important if your repository is public as this
    could allow others to execute code from forks of your repository.\
    Click on “settings”, “actions” \> “runners” and click on your
    runner\
    \
    <img src="./images/media/image25.png"
    style="width:9.35511in;height:3.52441in" />

20) Click on the remove button, that should show the following pop-up.
    Ideally you should remove the runner with the command shown in the
    pop-up (change “config.sh” to “config.cmd” in case of windows), or
    you can

Also click on the “force remove this runner button”\
\
<img src="./images/media/image26.png"
style="width:8.4615in;height:5.95788in"
alt="Graphical user interface, text Description automatically generated" />\
\
<img src="./images/media/image27.png"
style="width:9.4058in;height:3.48594in"
alt="A blue screen with white text Description automatically generated" />