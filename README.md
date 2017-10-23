# Analysis_Scripts_unfolding_oct2017
Scripts to go from the final level DRAGON sample to the end of the LE Flux unfolding 


1)Pickle the final level i3 files of the Dragion sample with the script named 'any_condenser...'. Script curtosy of Joao Pedro. M.
    items changed in the script 1) bdt cut changed from 0.1 to 0.2 (which was also done in the DRAGON analysis) for better data/mc agreement
                                2) mn_stop_containment is calculated but no longer used. we do not cut on this (we keep start containment)                                   this gains us some high energy events (~2000)
                                
2) May need to add scattering keys for newer oscfit. Use a version of Juan Pablo Yanez's 'produce_pickle_files.py' found in oscfit/resources

3) reweight the spectrum using DRAGON sample's 'no_weight' which contains: nu/antinu ratio, number of files, (ie oneweight stuff) but no particular flux model). For this 
- > use the scripts in:  'flux_reweight_package'.  See the README inside this folder for details

4) switch to oscfit_v2.03D_tania.  This oscfit is the same as oscfit_v2.03D, but instead of two weights (weight_e and weight_mu) for example, this version expects three weights (weight_e, weight_mu_k, weight_mu_pi), to two weights for the muons. the flux tables for weight_mu_k and weight_mu_pi were created with MCEq (with help from A. Fedynitch) and replace the 'up_to_horiz' or 'up to horizontal' flux systematic in oscfit. the up to horizontal shape is expected to come from differenes in pion decay rates at different zenith angles (mostly) and from the pion/kaion ratio.  A quantity called 'nu_pi_scale' is added instead so that the pion tempate can be scaled up and down (globally) by the fit to represent the total numu flux. 
- >  look at oscfit_v2.03D_tania

4) Now use a slightly hacked version of oscfit inorder to create a systematics.pckl file. The sustematics functions will be calculate and saved.  Load this file in the future instead of the actual systematics files. This resduces the about (GB) Of files you need to load drastically and makes is much easier to run oscfit instances on a server. This is important in this analysis as we need to run as many dataloaders (instances ) as we want to have bins in the unfolding. Please see Berlin Collaboration meeting talk or the tech note on this analysis for details). 
 - > switch to oscfit called Dragon_at_home from this git database
  - > use this script to create your systematics.pckl file

5) Now use a differnent slightly hacked version of oscfit that has a dataloader for each slice of true energy
  - > use this fitting script (it also makes psudo data)
