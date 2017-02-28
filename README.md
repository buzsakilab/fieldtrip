# FIELDTRIP

This is a version of the FieldTrip (FT) toolbox (http://www.fieldtriptoolbox.org/) that include iput/output fuctions for Neuroscope data formats (.eeg, .clu, .res, etc). It has been modify respect the offcial FieldTrip release.

The following is an example code to read and .xml and .eeg files:

ft_defaults; % set FT default global variables and path settings

hdr = ft_read_header([PathName basename '.xml'], 'headerformat', 'neuroscope_xml'); % load parameters from .xml file 
eegfile = ([PathName basename '.eeg']);

cfg = []; % FT configuration structure
cfg.datafile = ([PathName basename '.eeg']);
cfg.dataformat = 'neuroscope_bin'; 
cfg.headerformat = 'neuroscope_bin';
cfg.channel=hdr.label([10 20 30]); % load only these specific channels
% to perform a band-pass filter
cfg.hpfilter = 'yes'; cfg.hpfreq = 25;   
cfg.lpfilter = 'yes'; cfg.lpfreq = 200; 
lfp_filt = ft_preprocessing(cfg);
