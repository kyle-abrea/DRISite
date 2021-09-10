# READ ME:

# To install Vue:
First, download the latest version of Node from here: https://nodejs.org/en/download/. Then, go into the terminal and type:
```
npm install -g @vue/cli
```

# To create a project in Vue:
Go into the terminal and type:
```
npx @vue/cli create dri-site
```
The terminal will now ask you which version of Vue you would like: Vue 2 or Vue3. For this assessment, I chose Vue 2. <br/>
(Note: If you have Vue and Node installed already, the above two steps aren't necessary. Just clone the repo into your computer and run the already created project if this is the case.)

# Running the web page for the assessment:
In your terminal, cd into the project directory, in this case dri-site. Then, run it:
```
cd dri-site
npm run serve
```
If all goes well, the terminal will prompt you with two links. Choose the one that says Local, and then copy that link into your browser. This should render the webpage for assessment.

# Error handling:
When you first try to run the project, your terminal might say something like:
```
'vue-cli-service' is not recognized as an interntal or external command.... etc....
```
To fix this, type into your terminal:
```
npm i
```
Then, run the project again.