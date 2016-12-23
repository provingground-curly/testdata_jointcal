jointcal test data
==================

This repository contains data to test the performance of the [jointcal](http://github.com/lsst/jointcal) product.

Individual sets of testing data should be placed in their own directories, as butler-accessible repositories. They can then be loaded in testing code via the butler and the catalogs fed to jointcal. The image HDUs in the calexps in each repo have been set to identically zero and then compressed to save space, since the calexps are only needed for the calexp_md metadata.

The directories contained in this repository are listed below, with a description of their contents.

twinkles1
---------

Twinkles is a synthetic survey produced for the Dark Energy Science Collaboration's first data challenge. The intent with Twinkles is to test detection and analysis of type Ia SNe and strongly lensed quasars. Stars, galaxies and solar system objects were drawn from the LSST universe model. In addition to the standard universe, higher than natural rates of both type Ia SNe and lensed quasar systems were planted in the images. This repository includes one chip for the first 10 r-band visits in a deep drilling field (all observations are on the same night). See [here](https://github.com/DarkEnergyScienceCollaboration/Twinkles/blob/master/doc/Design.md) for a more complete description of the full survey.

**Note:** the calexps contained in this repository are identically zero and compressed and are only included for their metadata to build the `calexp_md`. If you want to use the twinkles images, please use the link above for details.

twinkles1_and_index
-------------------

Astrometry index catalogs corresponding to the twinkles1 data.

cfht
----

Source catalogs, metadata, and zeroed+compressed images derived from `validation_data_cfht`, processed with a version of the stack that provides VisitInfo (afw post-`tickets/DM-8052` merge: git hash 22f008f).

Then the `icExp/`, `icSrc/`, and `srcMatch` directories were deleted from `cfht/` and the calexps were processed via the included `compress_jointcal_cfht_test_data.py` to remove the pixel-level data and gzip compress them to make their size reasonable. I saved a skyMap to deepCoadds, generated by running:

```
makeDiscreteSkyMap.py cfht --output cfht/deepCoadd --id visit=850587^840375 ccd=12 --configfile makeSkyMapConfig.py
```

and this makeSkyMapConfig.py,

```
config.skyMap.projection='TAN'

# dimensions of inner region of patches (x,y pixels)
config.skyMap.patchInnerDimensions=[4000, 4000]

# nominal pixel scale (arcsec/pixel)
config.skyMap.pixelScale=0.185
```

cfht_and_index
--------------

Astrometry index catalogs corresponding to the cfht data.

decam
-----

Source catalogs, metadata, and zeroed+compressed images derived from `validation_data_decam`, processed with a version of the stack that provides VisitInfo (afw post-`tickets/DM-8052` merge: git hash 22f008f).

The `bkgd/`, `icMatch/`, and `icSrc/` directories were deleted from the visit sub-directories and the calexps were processed via the included `compress_jointcal_decam_test_data.py` to remove the pixel-level data and gzip compress them to make their size reasonable. I saved a skyMap to `deepCoadds/`, generated by running:

```
makeDiscreteSkyMap.py cfht --output data/deepCoadd --id visit=0176837^0176846 --configfile makeSkyMapConfig.py
```

and this makeSkyMapConfig.py:


```
config.skyMap.projection='TAN'

# dimensions of inner region of patches (x,y pixels)
config.skyMap.patchInnerDimensions=[4000, 4000]

# nominal pixel scale (arcsec/pixel)
config.skyMap.pixelScale=0.263
```

decam_and_index
---------------

Astrometry index catalogs corresponding to the decam data, copied from `validation_data_decam/astrometry_net_data/`.


Git LFS
-------

To clone and use this repository, you'll need Git Large File Storage (LFS).

Our [Developer Guide](http://developer.lsst.io/en/latest/tools/git_lfs.html)
explains how to set up Git LFS for LSST development.
