# Test data for OpenPTV "cavity"

This is a set of data measured using 3D-PTV method and kept in a working folder suitable
for the OpenPTV software (www.openptv.net)

## How to use it

    git clone https://github.com/alexlib/test_cavity_myptv
    python workflow.py <YAML> <COMMAND>
    

## Source of this data and credits

This set of data is recorded at the Alex Liberzon laboratory at the School of Mechanical 
Engineering, Tel Aviv University, http://turbulencelab.sites.tau.ac.il by the team of Reut Elfassi, 
David Ratner and Mark Kreizer (all Master students at that time) 

The setup is a lid-driven cavity in a cubic cavity of a 1:1:1 ratio. The top lid is a 
plastic belt driving system constructed for our laboratory by the I.T.E.S. 
http://www.ites.co.il/index.html

The 4 cameras are located on two sides of the cavity (positive and negative 'z'). More 
details are available from the Reut Elfassi (Kramer) thesis. 



## Processing with OpenPTV

1. Install PyPTV as explained in the OpenPTV documentation, see https://www.openptv.net
2. Run PyPTV using `pyptv test_cavity_myptv`
3. Follow the Youtube tutorial, links are on the OpenPTV documentation 
## Processing with MyPTV

1. install an updated MyPTV version in your virtual environment and copy `worflow.py`

        conda create -n myptv python=3.9 -y
        conda activate myptv
        git clone git+https://github.com/ronshnapp/myptv
        pip install myptv/setup.py -e . 

2. Following the `user_manual.pdf` instructions from https://github.com/ronshnapp/myptv/releases:
    we better use the file inside the Git preserved folder and not it's copy:

        cd example
        python ../myptv/example/workflow.py calibrate_cam1.yml calibration

3. Modifying `params_file.yml`:
    - renamed all `Calibration` to `cal`
    - renamed target file 
    - creating `cal_points1_full` (which is a combination of our `man_ori.par` and `man_ori.dat`, but with 6 points instead of 4) done manually, using `matplotlib`, see the `create_6_points.ipynb`
    - run `python workflow.py params_file.yml match_target_file` 

## License

`BY-SA` – [Attribution-ShareAlike](https://github.com/idleberg/Creative-Commons-Markdown/blob/master/4.0/by-sa.markdown)
