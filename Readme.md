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

4. Calibration:
    a) creting initial files: cam.ori: run the code without cam.ori file present

    python ../myptv/example/workflow.py .\calibration_cam1.yml calibration

    b) run again without the 6points_cal1 present - you get the GUI to pick 6 points
       pick and type the 3D coordinates - quite smart and faster probably then openptv. 

    c) run on 6 points file, tune the calibration to 1 - 2 pixels



5. Segmentation of the calibration target file

    python ../myptv/example/workflow.py .\calibration_cam1.yml segmentation

6. Match target

    python ../myptv/example/workflow.py .\calibration_cam1.yml match_target_file

7. calibration again, replace the `6points_cal1` by `blobs_cal1`
    - using `blobs_cal1` you should get about .5 pixel

8. Segmentation (had to rename all files to .tif)
    a) one image, Num_images = 1
    b) multiple images, change Num_images to N

    python ../myptv/example/workflow.py .\segmentation_cam2.yml segmentation



## License

`BY-SA` – [Attribution-ShareAlike](https://github.com/idleberg/Creative-Commons-Markdown/blob/master/4.0/by-sa.markdown)
