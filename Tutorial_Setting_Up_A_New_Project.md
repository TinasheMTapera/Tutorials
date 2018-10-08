# Tutorial: Setting Up A New Project

BBL lab members and affiliates work on a number of varied projects and can come from a range of backgrounds. It can be difficult to communicate, collaborate, and share our knowledge if we don't speak a common language; hence, it would be helpful to implement a few systems of uniformity that help us interact. In this tutorial, we demonstrate the typical directory structure of a new project including the recommendations for using git (or your preferred version control system).

# Part 1: The Directory Structure

**NB: Before you set this up, remember that we do not disclose PHI on Github or any other public forum. It's important to use a .gitignore file to make sure that we don't accidentally disclose PHI. Read this entire document first before you push anything to a Github repository.**

It's important to have a template for directory structure; this makes it easy to navigate foreign projects, transfer projects over to others, or simply for your own organizational benefit. Here's the recommended directory structure for BBL projects:

```
myproject/							# the project directory; the home of your project
|
+-- Notebook_n.ipynb		# your analysis notebooks (.ipynb, .rmd) live in the project directory
|
+--	scripts							# any scripts you write to automate large processes go in the scripts directory
|	|
|	+-- script1.sh
|	|
|	+-- script2.py
|
+-- data								# any data sources you work with for the project, such as .csv
|	|											# files, .dicom files, etc. that you read into your project notebook(s)
|	+-- participants.csv	# go into the data directory
|
+-- results							# the results directory contains any useful results outputs
	|											# from your notebooks or scripts, such as long .csv's, plots,
	+--	scan_results.csv	# or images that are too verbose for a notebok; ideally, you might
	|											# create a new notebook where you comment on and analyze your results
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
      +-- demographics 							# a demographics directory for all the demographics info
      |	  |
      |	  +-- participant_ids.json
      |	  :
      |   +-- contact_info.json
      |
      +-- scans 										# a scans directory for dicoms
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
+-- Struct_analysis.ipynb						# the first analysis
|
+-- Struct_analysis_GAM.ipynb				# the same analysis but using a GAM instead of GLM
|
+-- Struct_analysis_GAM_20181008.ipynb	# the same analysis but modified on today's date
|
+--	scripts/
|
+-- data/
+-- results/
```

If you're sure that the old versions of a notebook are obsolete, it is fine to delete them so that your project directory doesn't become bloated. It only helps to keep multiple notebooks so that:

-1 Your train of thought is consistent and compartmentalized
-2 Your analyses don't become too long

There are many benefits to using notebooks in [Python](https://unidata.github.io/online-python-training/introduction.html) or [R](https://www.r-bloggers.com/why-i-love-r-notebooks-2/) as opposed to a smattering of short scripts and notes files. They're highly recommended.

# Part 2: Git, Github, & .gitignore

We want to document our work online, as there are many benefits to this to the lab; we also want to maintain version control that we can go back to different versions of a project. However, we do not want to violate HIPPA and/or disclose PHI. Therefore, when using git, it's important to use a `.gitignore` file in order to make sure that git never puts PHI onto Github. Generally speaking, PHI will likely be in the `data` and `results` directories. We'll talk about it first before we get into git, since it's very important not to skip this step.

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
echo ".data/" >> .gitignore #to create a .gitignore that ignores the data directory
```

## What About the Git Repository?

Now that we've covered how to structure your project directory and how to ignore sensitive data, we have to talk about git itself. Git is a version control system used to track file changes and allow collaboration. Github is a publicly accessible repository where you can store and share your git repository so that others may see it, clone it, and work on it alongside you or on their own. 

It's recommended to initialize your repository in your projects folder, like so:

```
myproject/									# the project directory; initialize git here so as to capture 
|														# everything that happens with your project in version control,
+-- Notebook_n.ipynb				# but also create .gitignore here, hiding 'data' and 'results'
+--	scripts/				
+-- data/
+-- results/
```

See [this tutorial](https://www.atlassian.com/git/tutorials/setting-up-a-repository) on how to initialize a git repository, and see [here](https://www.atlassian.com/git/tutorials/what-is-git) to learn more about what git is.

# Conclusion

This tutorial covered recommended directory structure in BBL, including why it's important to have a uniform directory structure across projects and why we use notebooks. We also covered a little bit of git and how to organize your directories with git, including how to use the `.gitignore` file to hide sensitive data from public repositories.

Here is a .gitignore template with common filetypes we want to ignore in BBL: [template](./.gitignore)