# Problem Set 1

Your goal is to replicate a figure shown in a NY Times story on overdose deaths in the US. Here is a [link](https://www.nytimes.com/interactive/2016/01/07/us/drug-overdose-deaths-in-the-us.html) to that story (here is the [PDF](assets/How%20the%20Epidemic%20of%20Drug%20Overdose%20Deaths%20Rippled%20Across%20America%20-%20The%20New%20York%20Times%20(1).pdf)). Below, I'm attaching a screenshot of the "target" figure you have to replicate.

More specifically, you should:

Generate a single multi-panel figure with 3 rows and 6 columns showing overdose deaths for years 1999 through 2016.

The figure should include a (custom) color scale at the top of the figure with the title. 

You should use a similar color scale.

You should include the year number in the lower right corner of each panel.

Extra Credit: Make the figure interactive in some way, either through using ipywidgets or perhaps plotly.

Download the data on overdose deaths for each US county and year from the Centers for Disease Control and Prevention (CDC) website on [this](https://data.cdc.gov/NCHS/NCHS-Drug-Poisoning-Mortality-by-County-United-Sta/p56q-jrxg) link (click on "Export" on the top right corner, then "CSV").
Write your code in python in a Jupyter Notebook that is replicable on any computer.
 

## Submission instructions: 

You should submit a single zip file with ALL the necessary files (readme file, folders, script files, raw data, and output figure). The file should include instructions to run your code on any computer. 

- This includes the inclusion of a conda environment file so that it is reproducible. 
    - To create a conda environment file for export, go to a terminal, activate the conda environment you want to export and type:
        - `conda env export --no-builds`
        - This will export your environment to the terminal, which you can copy-paste to a file called environment.yml and add to your zip file.
        - **Recommended**: If you want to immediately write your environment to a yml file, type:
            - `conda env export --no-builds --file environment.yml`
            - But remember where you saved it!

If you have syntax issues, check the geopandas plot help: [https://geopandas.org/en/stable/docs/user_guide/mapping.html](https://geopandas.org/en/stable/docs/user_guide/mapping.html).

### Note about using LLMs

I know that it is tempting to try to just put this problem set into an LLM and get the right answer. I *strongly* advise you not to do that. I would rather that you come to me with issues and we can work them out together. LLMs will always be here, but you need to build a foundation of knowledge or else your vibe-coding will eventually come back to haunt you. 

## Grading

- Replicability: Your code is replicable on any computer without adding/editing the script file(s).
- Similarity: Your figure looks very similar to that of the NY Times article.
- Coding: Your code is well-written and follows efficient coding principles discussed in class.


![](assets/NYT%20screenshot.png)
