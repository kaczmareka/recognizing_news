In this folder, files used or produced by further experiments are stored. Not all of them were described in our work. To reproduce some of the experiments, installing more dependencies that are not present in the `requirements.txt` files might be necessary. 

## Structure of this folder

* `first_results` - directory with results from several experiments, mainly from GPT models.
* `notebooks` - directory with experiments for several other attempts to solve the problem stated in this work.
* `results` - a directory containing a few files with a summary of the results of the experiments that were conducted.
* `Final_pipeline_with_incidents.ipynb` - a notebook with the final pipeline, including examples of recognized incidents.

## Incidents recognition

In the initial steps of this work, several different attempts were also considered, including the Llama model or incident recognition problem, described below.

The aim was to find the information in the text, which was the main one described. It could be, e.g. `oil spill on the ocean` or `workplace racism`. Due to the results not being satisfactory, they were not further described. Some examples can be found in the `other_experiments/Final_pipeline_with_incidents.ipynb` file.