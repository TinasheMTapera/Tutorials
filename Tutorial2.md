# Setting Up A New Project: Directory Structure & gitignore
***
*Author*: Tinashe M. Tapera

*Date*: 8 October 2018

***

BBL lab members and affiliates work on a number of varied projects and can come from a range of backgrounds. It can be difficult to communicate, collaborate, and share our knowledge if we don't speak a common language; hence, it would be helpful to implement a few systems of uniformity that help us interact. In this tutorial, we demonstrate the typical directory structure of a new project including the recommendations for using git and Github in the lab.

# Table of Contents

1. [The Directory Structure](#Part 1: The Directory Structure)
2. [Git & `.gitignore`](#Part 2: Git, Github, & .gitignore)
3. [Project Setup Walkthrough](#Part 3: Project Setup Walkthrough)
4. [Conclusion & Template Link](#Conclusion)

# Part 1: The Directory Structure

**NB: Before you set this up, remember that we do not disclose PHI on Github or any other public forum. You must use a .gitignore file to make sure that we don't accidentally disclose PHI. Read this entire document first before you push anything to a Github repository.**

It's important to have a template for directory structure; this makes it easy to navigate foreign projects, transfer projects over to others, or simply for your own organizational benefit. Here's the recommended directory structure for BBL projects:

```
myproject/			        # the project directory; the home of your project
|
+-- Notebook_n.ipynb		        # your analysis notebooks (.ipynb, .rmd) live in the project directory
|
+--scripts			        # any scripts you write to automate large processes go in the scripts directory
|	|
|	+-- script1.sh
|	|
|	+-- script2.py
|
+-- data		                # any data sources you work with for the project, such as .csv
|	|		 	        # symlinked files, .dicom files, etc. that you read into your project notebook(s)
|	+-- participants.csv	        # go into the data directory
|
+-- results			        # the results directory contains any useful results outputs
	|			        # from your notebooks or scripts, such as long .csv's, plots,
	+-- scan_results.csv	        # or images that are too verbose for a notebook; ideally, you might
	|				# create a new notebook where you comment on and analyze your results
	+-- scan_plot.png
```

As you can imagine, it is very easy to navigate others' work if we are all structuring our directories in this way.

## Subdirectories

It's appropriate to create subdirectories within the 3 main directories `scripts`, `data`, and `results`. However, be sure to name them clearly so that others know why you've split them this way.

```

../
  |
  +-- data
      |
      +-- demographics 		        # a demographics directory for all the demographics info
      |	  |
      |	  +-- participant_ids.json
      |	  :
      |   +-- contact_info.json
      |
      +-- scans 			# a scans directory for dicoms
      	  |
      	  +-- p1_scan_01.dicom
      	  +-- p1_scan_02.dicom
      	  :
      	  +-- pn_scan_0n.dicom
```

## Notebooks and Versions

Version control allows us to go back to different versions of a file. This is different, however, from different analyses. Including a data transformation or using different data source is changing the analysis, not the version of it, and so it may be useful to create a new analysis notebook. In JuPyteR and R notebooks, simply duplicate the old notebook at the project directory level, and rename the notebook with an updated date or added change. In your notebook's first text block/cell, make a comment that this analysis carries on from a previous notebook.

```
myproject/
|
+-- Struct_analysis.ipynb		# the first analysis
|
+-- Struct_analysis_GAM.ipynb		# the same analysis but using a GAM instead of GLM
|
+-- Struct_analysis_GAM_20181008.ipynb	# the same analysis but modified on today's date
|
+-- scripts/
|
+-- data/
+-- results/
```

If you're sure that the old versions of a notebook are obsolete, it is fine to delete them so that your project directory doesn't become bloated. It only helps to keep multiple notebooks so that:

1. Your train of thought is consistent and compartmentalized
2. Your analyses don't become too long

There are many benefits to using notebooks in [Python](https://unidata.github.io/online-python-training/introduction.html) or [R](https://www.r-bloggers.com/why-i-love-r-notebooks-2/) as opposed to a smattering of short scripts and notes. They're highly recommended.

# Part 2: Git, Github, & .gitignore

Git is a version control system used to track file changes and allow collaboration. Github is a publicly accessible repository where you can store and share your git repository so that others may see it, clone it, and work on it alongside you or on their own. We want to document our work online, as there are many benefits of this to the lab; we also want to maintain version control that we can go back to different versions of a project. However, we do not want to violate HIPPA and/or disclose PHI. Therefore, when using Github, it's important to use a `.gitignore` file in order to make sure that git never puts PHI onto Github. Generally speaking, PHI will likely be in the `data` and `results` directories. We'll talk about it first before we get into git, since it's very important not to skip this step.

## How Does .gitignore Work?

When you use git for version control, a hidden file is created called `.gitignore`. This file is basically a list of the files that should not be tracked, staged, pushed, etc. It's used to maintain privacy from public repos and keep local changes local. A simple `.gitignore` file might look like this:

```
# ignore all Jupyter Notebook files
.ipynb_checkpoints

# ignore all IPython files
profile_default/
ipython_config.py

# ignore all pyenv files
.python-version

#etcetera
```

You can specify any file type in the .gitignore file. Git also supports \*nix notation and regular expressions, so you can use directories and regex to ignore files in different ways:

```
# ignore everything in the data folder; note the ending "/"
data/

# ignore all files containing the word "participant"
*participant*
```

Note that `.gitignore` doesn't automatically ignore itself, and so does show up in your Github repo. Therefore, you must be deliberate about what you ignore so as not to accidentally disclose PHI, while trying not to disclose PHI.

There are lots of templates available for ignoring particular files/directories with different programming project types. See [here](https://github.com/github/gitignore). More on `.gitignore` [here](https://swcarpentry.github.io/git-novice/06-ignore/)

## Creating a .gitignore

To create a `.gitignore` file in your repository, just type into any editor or use the terminal/command line; simply name it `.gitignore`.
```
echo "data/" >> .gitignore #to create a .gitignore that ignores the data directory
```

# Part 3: Project Setup Walkthrough

Now that you know your project directory structure, what you want to publish to Github, and what you must ignore from publishing, we can start a project. Follow these steps as they are the most straightforward and will have the least amount of overhead when it comes to configuration the bits and pieces.

0. Create SSH Key

In CHEAD, create an ssh key that will allow Github to communicate with your git directory. *This step is only necessary once*, and once it's done, your key persists until you remove it. See [here](https://jumpcloud.com/blog/what-are-ssh-keys/) for more on ssh keys.

First, log into CHEAD:

```
ssh -Y YOUR-USERNAME@chead
```

Then, input this command:

```
ssh-keygen
```

The above command will initiate the process of generating a private, secure key that will allow crosstalk with Github. Press `enter` when asked where to place the file (i.e. leave it in the default location), and using a passphrase is optional. You'll notice after this that a hidden directory in your home folder is created `~/.ssh`, and in it, are two files `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`. Open the second file for viewing:

```
cat `~/.ssh/id_rsa.pub`
```

Copy everything in this file to your clipboard. Now, go back to Github, and in the top-right, click on your profile button, and in the drop-down, click **Settings**.

In the settings page, select **SSH and GPG Keys** on the left, and click the green button **New SSH Key**. In the **Key** box, paste the SSH data you just copied from CHEAD, and give your SSH key a relevant title like "CHEAD-Key1". Click **Add SSH Key** to finish this step.


1. Create the Empty Github Repository

You'll start by creating an empty repo on Github. In the [PennBBL organization Github](https://github.com/PennBBL), click the green button **New** (if you don't see it, ask to be added to the organization with the right permissions from a supervisor). Name and describe the repository whatever you'd like, so long as it is descriptive. Keep the repository as public, and tick the box for "Initialize this repository with a README". No .gitignore or license is necessary yet. Click **Create Repository**. There should be a new repository with an empty README file.

2. Clone the Github Repository to Your CHEAD

In Github, click the green **Clone or Download** button, and in the dropdown, click *Use SSH*; copy the string `git@github.com:PennBBL/<<MYPROJECT>>.git` to your clipboard.

Go to the directory in CHEAD where you'd like your project to live. In this directory, type `git clone git@github.com:PennBBL/MYPROJECT.git`. There should be a new subdirectory called MYPROJECT (whatever your project is called on Github) now that you can work in, with an empty README file.

3. The All-Important `.gitignore`

Now, it's recommended to take the necessary steps to mask PHI from publication and setup your `.gitignore` file *BEFORE* you add anything important. We recommend first starting out with a test. Set your directory up as below, and create two test files; one that would live in a PHI directory, and one that wouldn't.

```
MYPROJECT
|
+-- scripts/
+-- data/
+-- results/
```

You may want to move patient files to `data/`, which means it will contain potential PHI. Test this first by adding one file to the `data` directory, one file to the `scripts` directory, and then adding the `data` directory to your `.gitignore`, either using an editor, or appending to a file:

```
echo "THIS IS NOT PHI AND CAN BE PUBLISHED" >> scripts/TEST.txt
echo "THIS IS PHI" >> data/TEST.txt
echo "data/" >> .gitignore
```

4. Test Git

Now, test if your procedure works. Type the following command:

```
git status
```

This command asks the version control to report on what changes it has seen. If you've done this correctly, git will report back that there has been a `.gitignore` added, and `scripts` and `results` directories added. **Note that the `data` directory is not being tracked.**

Use the `add` command to ensure git adds this new content to its list of files to track.

```
git add . #use a period to add everything, regex to glob multiple files, or add files by name
```

Next, commit these changes to the git repository, like creating a save point that you could come back to if need be.

```
git commit -m "this is my test commit"
```

Finally, if you're happy with your work, you can push these changes to Github to publish them for others to see and access.

```
git push origin master
```

Check your now updated project on Github! From here, you can go back to CHEAD and do whatever work you need, hiding PHI with a .gitignore, writing scripts and analysis notebooks, and publishing your work to Github. using `add`, `commit`, and `push`.

# Conclusion

This tutorial covered recommended directory structure in BBL, including why it's important to have a uniform directory structure across projects and why we use notebooks. We also covered a little bit of git and how to organize your directories with git, including how to use the `.gitignore` file to hide sensitive data from public repositories. Lastly, we practiced the best method of setting up a git repository for your projects on CHEAD, as well as how to publish your work on Github. See [here](https://www.atlassian.com/git/tutorials/what-is-git) to learn more about what git is.

Here is a .gitignore template with common filetypes we want to ignore in BBL: [template](https://github.com/PennBBL/tutorials/blob/master/code/.gitignore)
