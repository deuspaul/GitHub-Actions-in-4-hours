**Exercise \#5: Deploy** 

1)  Make sure you have NPM installed in your system, if you don’t have
    it installed follow the documentation:
    https://nodejs.org/en/download/

2)  Next open a terminal/powershell/cmd as administrator and install
    surge: npm install --global surge

3)  Next run: “surge” in terminal/powershell/cmd. If you get an error
    message about scripts being disabled in the system, run the
    following to bypass scripts for the process:\
    Set-ExecutionPolicy bypass -Scope Process

<img src="./images/media/image64.png"
style="width:9.13299in;height:3.88553in"
alt="A blue screen with white text and red and yellow text Description automatically generated" />

4)  It should ask you for your email, and to create a password.\
    You should receive an email to activate your account.\
    It should ask you for a project location, for this you can create a
    new folder or select an empty folder.\
    Then it should provide you with your url:\
    \
    <img src="./images/media/image65.png"
    style="width:4.98958in;height:1.07292in"
    alt="A blue screen with white text Description automatically generated" />

5)  Next generate a token with the command:\
    surge token

6)  Open the project from the previous exercise (the one we forked) and
    click on “settings”. Then within the “Code and automation” section
    click on “environments” and click on “New environment”. Name it
    “production” and do not add any protection rules.\
    \
    <img src="./images/media/image66.png"
    style="width:8.95063in;height:4.12925in" />

7)  Next, click on “Add Secret” within “Environment Secrets” and create
    the following:\
    SURGE_LOGIN (Input the email address for your surge account)\
    SURGE_TOKEN (paste the token that we copied on step \#5)\
    \
    <img src="./images/media/image67.png"
    style="width:9.2666in;height:8.78712in"
    alt="A screenshot of a computer Description automatically generated" />

8)  Next let’s edit our workflow to deploy our application. Create a new
    job and add the following:\
    Replace the url with your url from surge (without the “\<” and “\>”
    symbols)\
    \
    deploy:\
    runs-on: ubuntu-latest\
    needs: build\
    environment:\
    name: production\
    url: http://\< replace-with-your-surge-url\>.surge.sh\
    \
    <img src="./images/media/image68.png"
    style="width:4.05208in;height:1.375in"
    alt="A screen shot of a computer Description automatically generated" />

9)  Now we are ready to add the steps. Let’s download the build artifact
    from the “build” job.\
    \
    steps:\
    - name: Download the Build Artifact\
    uses: <actions/download-artifact@v4.1.2>\
    with:\
    name: build

10) Next, lets deploy our application. Add another step with the
    following code:\
    Replace the domain with your url from surge (without the “\<” and
    “\>” symbols)\
    \
    - name: deploy to surge\
    run: npx surge --project '.' --domain \<
    replace-with-your-surge-url\>.surge.sh\
    env:\
    SURGE_LOGIN: \${{ secrets.SURGE_LOGIN }}\
    SURGE_TOKEN: \${{ secrets.SURGE_TOKEN }}

<img src="./images/media/image69.png"
style="width:5.97917in;height:3.55208in"
alt="A computer screen shot of a program Description automatically generated" />

11) Change the trigger from “workflow_dispatch” to “push: branches:
    -main”\
    \
    on:\
    push:\
    branches:\
    - main

<img src="./images/media/image70.png"
style="width:2.89583in;height:1.15625in"
alt="Graphical user interface, text Description automatically generated with medium confidence" />

12) Click on “start commit” and commit directly to main branch

13) This will automatically trigger our workflow from now on every
    timewe make changes on the main branch\
    \
    <img src="./images/media/image71.png"
    style="width:9.06314in;height:3.20094in"
    alt="A screenshot of a computer Description automatically generated" />

14) And once the job finishes successfully, you should see your
    environment url in the deploy job:\
    \
    <img src="./images/media/image72.png"
    style="width:9.26458in;height:7.02406in"
    alt="A screenshot of a computer Description automatically generated" />\
    As well as in the main page of your repository:\
    \
    <img src="./images/media/image73.png"
    style="width:9.06377in;height:7.5017in"
    alt="A screenshot of a computer Description automatically generated" />