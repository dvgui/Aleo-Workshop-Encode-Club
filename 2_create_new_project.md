# 2 Create A New Token Project

## Create the project
To create a new project, we use the command `leo new <project_name>`

Make sure you are at the root folder of this repository when you are creating a new project. [You can use this repo to get started with completing the task to complete this workshop]

In this example, we will create a new token project:
```bash
leo new token_$RANDOM
```
You can also create the token with your custom name
```bash
leo new token_custom_name
```
Make sure everything is in lower case!

## Commands to run and test the project

Now that you have created the project, enter the project by:
```bash
cd token_...
```

Then run below code to build and run the program in `main.leo`.
```bash
leo run main 1u32 2u32 # Note that `main` here is the functions name in the program, not the file name.
```

You should see the output equal to `3u32`.

To learn more about the Aleo Project Interactions, check out [here](https://developer.aleo.org/leo/hello).

## Project Folder Outline

```bash
.
├── program.json # program description file
└── src # Folder for all Program source codes
    └── main.leo # define your program logic here
```
