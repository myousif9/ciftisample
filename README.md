# hipposample

Tool for sampling volume images across bids datasets to hippunfold surfaces.

## Usage
- `bids_dir` corresponds to `hippunfold` directory
- `derivatives` flag is used to provide volume images that are to be sampled
- `smoothing_kernel_mm` flag defines the size of smoothing kernel in millimeters
  

        ```
        python run.py /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/hippunfold/hippunfold/ \
        /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/hipposample participant \
        --derivatives /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/snakedwi/snakedwi \
        --profile cc-slurm-3hr \
        --singularity-prefix /project/6050199/myousif9/.kslurm/containers/snakemake \
        --smoothing_kernel_mm 1 2
        ```
- To specify alternative image to sample use either `filter-volume` or `path-volume` flags to specify that image
  - `filter-volume` flag usage example:
    
        ```
        python run.py /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/hippunfold/hippunfold/ \
        /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/hipposample participant \
        --derivatives /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/snakedwi/snakedwi \
        --profile cc-slurm-3hr \
        --singularity-prefix /project/6050199/myousif9/.kslurm/containers/snakemake \
        --smoothing_kernel_mm 1 2
        --filter-volume suffix=MD
        ```
    
  - `path-volume` flag usage example:
    
        ```
        python run.py /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/hippunfold/hippunfold/ \
        /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/hipposample participant \
        --derivatives /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/snakedwi/snakedwi \
        --profile cc-slurm-3hr \
        --singularity-prefix /project/6050199/myousif9/.kslurm/containers/snakemake \
        --smoothing_kernel_mm 1 2
        --path-volume /project/ctb-akhanf/myousif9/norm_models/datasets/AOMIC/ds003097/derivatives/snakedwi/snakedwi/sub-{subject}/dwi/sub-{subject}_space-T1w_res-orig_desc-eddy_dtifit/dti_MD.nii.gz
        ```



## CLI
```
usage: run.py [-h] [--pybidsdb-dir PYBIDSDB_DIR] [--pybidsdb-reset] [--force-output] [--help-snakemake]
              [--participant-label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]]
              [--exclude-participant-label EXCLUDE_PARTICIPANT_LABEL [EXCLUDE_PARTICIPANT_LABEL ...]] [--derivatives DERIVATIVES [DERIVATIVES ...]]
              [--skip-bids-validation] [--smoothing-kernel-mm SMOOTHING_KERNEL_MM [SMOOTHING_KERNEL_MM ...]]
              [--filter-volume FILTER_VOLUME [FILTER_VOLUME ...]] [--filter-inner FILTER_INNER [FILTER_INNER ...]]
              [--filter-outer FILTER_OUTER [FILTER_OUTER ...]] [--filter-mid FILTER_MID [FILTER_MID ...]]
              [--wildcards-volume WILDCARDS_VOLUME [WILDCARDS_VOLUME ...]] [--wildcards-inner WILDCARDS_INNER [WILDCARDS_INNER ...]]
              [--wildcards-outer WILDCARDS_OUTER [WILDCARDS_OUTER ...]] [--wildcards-mid WILDCARDS_MID [WILDCARDS_MID ...]] [--path-volume PATH_VOLUME]
              [--path-inner PATH_INNER] [--path-outer PATH_OUTER] [--path-mid PATH_MID]
              bids_dir output_dir {participant}
run.py: error: the following arguments are required: bids_dir, output_dir, analysis_level
(ciftisample_venv) [myousif9@gra-login3 hipposample]$ python run.py --help
App version not found; will be recorded in output as 'unknown'. If this is unexpected, please contact the app maintainer.
usage: run.py [-h] [--pybidsdb-dir PYBIDSDB_DIR] [--pybidsdb-reset] [--force-output] [--help-snakemake]
              [--participant_label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]]
              [--exclude_participant_label EXCLUDE_PARTICIPANT_LABEL [EXCLUDE_PARTICIPANT_LABEL ...]] [--derivatives DERIVATIVES [DERIVATIVES ...]]
              [--skip-bids-validation] [--smoothing_kernel_mm SMOOTHING_KERNEL_MM [SMOOTHING_KERNEL_MM ...]]
              [--filter-volume FILTER_VOLUME [FILTER_VOLUME ...]] [--filter-inner FILTER_INNER [FILTER_INNER ...]]
              [--filter-outer FILTER_OUTER [FILTER_OUTER ...]] [--filter-mid FILTER_MID [FILTER_MID ...]]
              [--wildcards-volume WILDCARDS_VOLUME [WILDCARDS_VOLUME ...]] [--wildcards-inner WILDCARDS_INNER [WILDCARDS_INNER ...]]
              [--wildcards-outer WILDCARDS_OUTER [WILDCARDS_OUTER ...]] [--wildcards-mid WILDCARDS_MID [WILDCARDS_MID ...]] [--path-volume PATH_VOLUME]
              [--path-inner PATH_INNER] [--path-outer PATH_OUTER] [--path-mid PATH_MID]
              bids_dir output_dir {participant}

Snakebids helps build BIDS Apps with Snakemake

options:
  -h, --help            show this help message and exit

STANDARD:
  Standard options for all snakebids apps

  --pybidsdb-dir PYBIDSDB_DIR, --pybidsdb_dir PYBIDSDB_DIR
                        Optional path to directory of SQLite databasefile for PyBIDS. If directory is passed and folder exists, indexing is skipped. If
                        pybidsdb_reset is called, indexing will persist
  --pybidsdb-reset, --pybidsdb_reset
                        Reindex existing PyBIDS SQLite database
  --force-output, --force_output
                        Force output in a new directory that already has contents
  --help-snakemake, --help_snakemake
                        Options to Snakemake can also be passed directly at the command-line, use this to print Snakemake usage

SNAKEBIDS:
  Options for snakebids app

  bids_dir              The directory with the input dataset formatted according to the BIDS standard.
  output_dir            The directory where the output files should be stored. If you are running group level analysis this folder should be
                        prepopulated with the results of the participant level analysis.
  {participant}         Level of the analysis that will be performed.
  --participant_label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...], --participant-label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]
                        The label(s) of the participant(s) that should be analyzed. The label corresponds to sub-<participant_label> from the BIDS spec
                        (so it does not include "sub-"). If this parameter is not provided all subjects should be analyzed. Multiple participants can be
                        specified with a space separated list.
  --exclude_participant_label EXCLUDE_PARTICIPANT_LABEL [EXCLUDE_PARTICIPANT_LABEL ...], --exclude-participant-label EXCLUDE_PARTICIPANT_LABEL [EXCLUDE_PARTICIPANT_LABEL ...]
                        The label(s) of the participant(s) that should be excluded. The label corresponds to sub-<participant_label> from the BIDS spec
                        (so it does not include "sub-"). If this parameter is not provided all subjects should be analyzed. Multiple participants can be
                        specified with a space separated list.
  --derivatives DERIVATIVES [DERIVATIVES ...]
                        Path(s) to a derivatives dataset, for folder(s) that contains multiple derivatives datasets (default: False)
  --skip-bids-validation, --skip_bids_validation
                        Skip validation of BIDS dataset. BIDS validation is performed by default using the bids-validator plugin (if installed/enabled)
                        or with the pybids validator implementation (if bids-validator is not installed/enabled).
  --smoothing_kernel_mm SMOOTHING_KERNEL_MM [SMOOTHING_KERNEL_MM ...], --smoothing-kernel-mm SMOOTHING_KERNEL_MM [SMOOTHING_KERNEL_MM ...]

BIDS FILTERS:
  Filters to customize PyBIDS get() as key=value pairs, or as key:{REQUIRED|OPTIONAL|NONE} (case-insensitive), to enforce the presence or absence of
  values for that key.

  --filter-volume FILTER_VOLUME [FILTER_VOLUME ...], --filter_volume FILTER_VOLUME [FILTER_VOLUME ...]
                        (default: suffix=FA extension=.nii.gz datatype=dwi)
  --filter-inner FILTER_INNER [FILTER_INNER ...], --filter_inner FILTER_INNER [FILTER_INNER ...]
                        (default: suffix=inner extension=.surf.gii space=T1w)
  --filter-outer FILTER_OUTER [FILTER_OUTER ...], --filter_outer FILTER_OUTER [FILTER_OUTER ...]
                        (default: suffix=outer extension=.surf.gii space=T1w)
  --filter-mid FILTER_MID [FILTER_MID ...], --filter_mid FILTER_MID [FILTER_MID ...]
                        (default: suffix=midthickness extension=.surf.gii label=hipp space=T1w)

INPUT WILDCARDS:
  File path entities to use as wildcards in snakemake

  --wildcards-volume WILDCARDS_VOLUME [WILDCARDS_VOLUME ...], --wildcards_volume WILDCARDS_VOLUME [WILDCARDS_VOLUME ...]
                        (default: subject session acquisition task run desc space suffix)
  --wildcards-inner WILDCARDS_INNER [WILDCARDS_INNER ...], --wildcards_inner WILDCARDS_INNER [WILDCARDS_INNER ...]
                        (default: subject session acquisition task run den desc hemi space label)
  --wildcards-outer WILDCARDS_OUTER [WILDCARDS_OUTER ...], --wildcards_outer WILDCARDS_OUTER [WILDCARDS_OUTER ...]
                        (default: subject session acquisition task run den desc hemi space label)
  --wildcards-mid WILDCARDS_MID [WILDCARDS_MID ...], --wildcards_mid WILDCARDS_MID [WILDCARDS_MID ...]
                        (default: subject session acquisition task run den desc hemi space label)

PATH OVERRIDE:
  Options for overriding BIDS by specifying absolute paths that include wildcards, e.g.: /path/to/my_data/{subject}/t1.nii.gz

  --path-volume PATH_VOLUME, --path_volume PATH_VOLUME
  --path-inner PATH_INNER, --path_inner PATH_INNER
  --path-outer PATH_OUTER, --path_outer PATH_OUTER
  --path-mid PATH_MID, --path_mid PATH_MID

```
