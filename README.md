# PyStacker

`PyStacker` is a wrapper that performs the spectral stacking code on either an existing `PyStructure` database or a set of 3D data cubes (fits files). When executing via the terminal the `-c` parameter sets the configure file and `-m` the mode.

## Instruction:

There exist two modes how the PyStacker code can be utilized:

1. **With a `PyStructure` Database**

> In case a database (as a `.npy` file) exists, the code can be executed by adjusting the parameters in the configur file as shown in `run_PyStructure.conf`. Then simply execute in the terminal with:
> ```
> python PyStacker.py -c run_PyStructure.conf -m PyStruc
> ```
> where `PyStruc` sets the mode on how to execute the program.

> **Note:** You can provide optional parameters (list: TBD). You can also simply remove these parameters (or add pre-existing optional parameters) at the end of the configure file.

2. **Only with 3D Fits Datacubes**
> The code now also works without a pre-existing PyStructure database. 3D Datacubes are required as input. These have to be convolved and regridded to the same resolution and the same grid. In addition, a velocity map with which to shuffle the spectra, must be provided. It can be executed by adjusting the parameters in the `run_3DCube.conf` file:
> ```
> python PyStacker.py -c run_3DCube.conf -m 3D_cube
> ```
> where `3D_cube` sets the mode on how to execute the program.

## Documentation:

#### Optional Parameters:
The configure file accepts a list of optional parmeters which make it possible to customize the stacking method.

> 'nbins': number of bins (integer). DEFAULT: 10
>
> 'xmin': bin minimum DEFAULT: set as minimum of data range
>
> 'xmax': bin minimum DEFAULT: set as maximum of data range
>
> 'bin_scaling': "linear" or "log" DEFAULT: "linear"
>
> 'sn_limits': S/N thresholds for lower and upper mask DEFAULT: [2,4]
>
> 'no_detec_wdw': window size over which to integrate for limit in case no detection is found. In km/s DEFAULT: 30
>
> 'pad_v':  in km/s range at either edges to exclude from integrating or finding the mask. DEAFULT: 100
>
> 'line_wdw': window size where emission is expected to exlude from finding the mask. In km/s DEAFULT:0
>
> 'ignore_empties': True or False, weither sightlines without datat hould be ignored. DEAFULT: False
>
> 'weights_type': string name of the quantity by which to weight the stacking. DEFAULT: None
>
> 'rms_type': How to measure the line rms can be 'iterative' or None (DEFAULT)
>
> 'trim_stackspec': Boolean, if true (DEFAULT), trim the stacked spectrum to only include channels, where the overlap of all spectra is given

#### Keys:

> 'beam_as': beam size (FWHM) in arcseconds (float)
> 
> 'vaxis_kms': velocity axis in km/s (numpy array) 
> 
> 'xtype': stacking quantity, i.e. quantity used to define the stacking bins (string)
> 
> 'xmin': stacking bins minima (numpy array)
> 
> 'xmid': stacking bins centers (numpy array)
> 
> 'xmax': stacking bins maxima (numpy array) 
> 
> 'spec_K_"line"': brightness temperature of the "line" data in units of kelvin corresponding to the velocity axis 'vaxis_kms' (numpy array)
> 
> 'rms_K_"line"': rms noise of the brightness temperatures computed as the standard deviation of the spectrum in the emission free channels, i.e. across channels not selected by the 'mask' (numpy array)
> 
> 'center_kms_"line"': center velocity of the "line" in each pixel computed from the prior line (numpy array)
> 
> 'peak_K_"line"': peak brightness temperature of the "line" in units of kelvin (numpy array)
> 
> 'ii_K_kms_"line"': integrated intensity of the "line" in units of kelvin times km/s, resulting from velocity integration of the stacked spectra across the velocity range selected by the 'mask' (numpy array)
> 
> 'uc_ii_K_kms_"line"': uncertainties of the integrated intensity of the "line" in units of kelvin times km/s following equation 3 from Neumann et al. 2023b
> 
> 'prior_mask': velocity integration mask (numpy array) 
> 
> 'upplim_K_kms_"line"': 3-sigma upper limit of the integrated intensities of the "line" in units of kelvin times km/s (numpy array)
> 
> 'lowlim_K_kms_"line"': lower limit of the integrated intensities of the "line" in units of kelvin times km/s, returned if the stacked spectrum extends over the full velocity range (numpy array)
> 
> 'SNR_"line"': signal-to-noise ratio of the integrated intensities of the "line", i.e. 'ii_K_kms_"line"'/'uc_ii_K_kms_"line"' (numpy array)
> 
> 'ncounts_"line"', number of prior-detected spectra inside each bin (numpy array)
> 
> 'ncounts_total_"line"': total number of spectra inside each bin (numpy array)
