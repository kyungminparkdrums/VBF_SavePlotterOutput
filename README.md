# SavePlotterOutput
Reads the output file from the **[BSM3G Plotter](https://github.com/BSM3G/Plotter)** in root format and save certain figures inside the root file as pdf, following the options given by user
  - **`saveFigures.py`**: Get a plotter output root file and a config file that contains the options for saving the figures from the plotter output. Then, save them as pdf files following the user options given in the config file. **PyROOT should be available to run this. Make sure your ROOT supports PyROOT**
      ```
         python saveFigures.py --config <config file> --input_file <input root file (output file from the Plotter)>
      ```
  - Running the line above will give you the certain histograms after certain cut step that you specified in the config file, in pdf format under the name of `<cut_step>_<histogram_name>.pdf`. Unless you specified the output pdf directory in the config file, i.e. `--output_dir <dir>`, these will be stored in `./output/` directory which will be automatically created.
  - **config**: i.e. `config/saveOptions.config`
    - Config file contains options for saving figures.
    - Mandatory options to be included in every line are as follows.
      ```
         --step <cut step> --kinematic <kinematic>
      ```
    - Additional options you can add are as follows.
      ```
         --year <year (to correct the lumi on the top right if necessary)>
         --isPreliminary <True ('Preliminary' below CMS logo) or False (default: 'Work in Progress' below CMS logo)>
         --output_dir <output directory (default: ./output/)>
         --legend_column <# of columns for the legend (default: 1)>
         --display_title <True or False (default: False)>
         --draw_without_ratio <True or False (default: False)>
         --set_logX <True or False (default: False)>
         --x_range <x axis range in list format>
         --x_title <x axis title in TLatex format>
         --set_logY <True or False (default: False)>
         --histo_y_range <stacked histogram y axis range in list format>
         --histo_y_title <stacked histogram y axis title>
         --ratio_y_range <ratio plot y axis range in list format>
      ```

    - **IMPORTANT**: when giving options for axis title, please note the followings (otherwise, it'll crash):
      - 1. if the title contains brackets, please put a backslash before opening and closing of the brackets, i.e. `p_{T}\(jj\)` instead of `p_{T}(jj)`
      - 2. if the title contains greek letters that require backslash in latex form, replace the backslash with hashtag, i.e. `#mu` instead of `\mu`
      ```
      # Example
      --step NDiMuonCombinations --kinematic DiMuonPt --x_range [0,300] --set_logY True --ratio_y_range [0.6,1.4] --legend_column 2 --year 2017
      --step NRecoBJet --kinematic Met --x_title p^{miss}_{T}[GeV] --histo_y_title Events --legend_column 1 --x_range [250,1000] --year 2017
      ```

```
# Example
python saveFigures.py --config ./config/saveOptions.config --input_file ./inputs/VBF_SUSY_0-lepton_2017_Z_CR1.root

```
