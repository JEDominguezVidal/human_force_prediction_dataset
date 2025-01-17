# Human Force Prediction Dataset

This repository contains a dataset designed for research in predicting human force exertion and human-robot pair velocity in a dynamic environment. The dataset includes training, validation, and testing splits, each capturing the evolution of input features over the last 2 seconds and corresponding outputs for the next 1 second, recorded at 10 Hz. Below, you'll find detailed information about the dataset structure, usage, and license.

## Dataset Overview

### Files and Sizes
- **train_dataset.h5**: 17,028 samples, 27.5 GB (compressed: 136 MB)
- **val_dataset.h5**: 946 samples, 1.5 GB (compressed: 7.6 MB)
- **test_dataset.h5**: 946 samples, 1.5 GB (compressed: 7.5 MB)

### Setup Description
This dataset was obtained in an indoor setup using the **TiaGO++ robot** by **PAL Robotics**, collaboratively working with different volunteers in a collaborative transportation task. The experiments were conducted across six different scenarios with multiple obstacles, and in all cases, at least two distinct routes were available to transport the object to the goal. For more information, refer to the articles listed in the References section or the following article:

- J.E. Domínguez-Vidal, N.A. Rodríguez, and A. Sanfeliu. *Perception–intention–action cycle in human–robot collaborative tasks: The collaborative lightweight object transportation use-case*. International Journal of Social Robotics, 2024, to appear.

### Structure of Each Sample
Each sample is divided into two groups:

#### Inputs (X)
- **Map**: 20 occupancy grids (100x100 pixels), with each cell taking values of 0 or 100 based on occupancy.
- **Human_force**: 20 samples of human-applied force (x, y components).
- **SFM_force**: 20 samples of Social Force Model (SFM) force (x, y components).
- **Velocity**: 20 samples of velocity (linear and angular components).
- **Distance_goal**: 20 samples of distance to the goal (magnitude and angle).

#### Outputs (Y)
- **Human_future_force**: 10 samples of human-applied force for the next second (x, y components).
- **Future_velocity**: 10 samples of velocity for the next second (linear and angular components).

## Usage

### Loading the Dataset
The dataset is stored in the HDF5 format, which can be accessed using Python's `h5py` library. Below is an example of how to load and explore the dataset:

```python
import h5py

# Load the training dataset
with h5py.File('train_dataset.h5', 'r') as h5file:
    # List all samples
    print("Samples:", list(h5file.keys()))

    # Access a specific sample
    case_id = list(h5file.keys())[0]  # Get the first case ID
    map_data = h5file[case_id]['X']['Map'][:]
    human_force = h5file[case_id]['X']['Human_force'][:]
    sfm_force = h5file[case_id]['X']['SFM_force'][:]
    velocity = h5file[case_id]['X']['Velocity'][:]
    distance_goal = h5file[case_id]['X']['Distance_goal'][:]

    # Outputs
    human_future_force = h5file[case_id]['Y']['Human_future_force'][:]
    future_velocity = h5file[case_id]['Y']['Future_velocity'][:]

    print("Map data shape:", map_data.shape)
    print("Human force shape:", human_force.shape)
    print("Human future force shape:", human_future_force.shape)
```

### Suggested Applications
This dataset can be used for:
- Developing and testing models for human force prediction.
- Simulating human-robot interaction scenarios.
- Studying dynamic environments and human behavior in navigation tasks.

## License
This dataset is released under the [MIT License](LICENSE). You are free to use it for both academic and commercial purposes, provided appropriate attribution is given.

## References
This dataset has been created and utilized in the following publications:

1. J.E. Domínguez-Vidal and A. Sanfeliu. *Force and velocity prediction in human-robot collaborative transportation tasks through video retentive networks*, 2024 IEEE/RSJ International Conference on Intelligent Robots and Systems, 2024, Abu Dhabi, UAE, pp. 9307-9313.
2. J.E. Domínguez-Vidal and A. Sanfeliu. *Exploring transformers and visual transformers for force prediction in human-robot collaborative transportation tasks*, 2024 IEEE International Conference on Robotics and Automation, 2024, Yokohama (Japan), pp. 3191-3197.
3. J.E. Domínguez-Vidal and A. Sanfeliu. *Improving human-robot interaction effectiveness in human-robot collaborative object transportation using force prediction*, 2023 IEEE/RSJ International Conference on Intelligent Robots and Systems, 2023, Detroit, MI, USA, pp. 7839-7845.

## Citation
If you use this dataset in your research, please cite it using any of the previous references:

```
@article{DominguezVidal2024_SORO,
  author    = {J. E. Dom{\'\i}nguez-Vidal and
               Nicol{\'a}s Rodr{\'\i}guez and
               Alberto Sanfeliu},
  title     = {{Perception--Intention--Action Cycle in Human--Robot Collaborative Tasks: The Collaborative Lightweight Object Transportation Use-Case}},
  journal   = {International Journal of Social Robotics},
  volume    = {},
  year      = {2024},
  number    = {},
  pages     = {1--30},
  doi       = {10.1007/s12369-024-01103-7}
}
```

```
@inproceedings{DominguezVidal2024_IROS,
  title={{Force and Velocity Prediction in Human-Robot Collaborative Transportation Tasks through Video Retentive Networks}},
  author={Dom\'{i}nguez-Vidal, J. E. and Sanfeliu, Alberto},
  booktitle={2024 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  pages={9307--9313},
  year={2024},
  organization={IEEE}
}
```

```
@inproceedings{DominguezVidal2024_ICRA,
  title={{Exploring Transformers and Visual Transformers for Force Prediction in Human-Robot Collaborative Transportation Tasks}},
  author={Dom{\'\i}nguez-Vidal, J. E. and Sanfeliu, Alberto},
  booktitle={2024 IEEE International Conference on Robotics and Automation (ICRA)},
  pages={3191--3197},
  year={2024},
  organization={IEEE}
}
```

```
@inproceedings{DominguezVidal2023_IROS,
  title={{Improving Human-Robot Interaction Effectiveness in Human-Robot Collaborative Object Transportation using Force Prediction}},
  author={Dom\'{i}nguez-Vidal, J. E. and Sanfeliu, Alberto},
  booktitle={2023 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  pages={7839--7845},
  year={2023},
  organization={IEEE}
}
```

## Contact
For questions or suggestions, please contact [jdominguez@iri.upc.edu].
