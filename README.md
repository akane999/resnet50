## ResNet50

#### Standard Parameter(s): 

1. `input-path`: Path to the location of the dataset. With the current version, 
it is recommended to use only one directory where all the data exists. 
The validation-training split is handled by the  `validation-split` 
parameter and the user does not need to handle it at the directory level

2. `epochs`: Number of epochs the model should train for.

3. `height`: Height of the image that should be fed into the model. This height is independent of the size of the dataset. The keras `ImageDataGenerator` class handles the resizing of these images.

4. `width`: Width of the image that should be fed into the model.

> Info: The minimum height and width for the resnet model is (30,30). Any value below this will raise an exception.

#### Optional Parameter(s): These parameters have a default value and therefore the script runs using them. Please note that these are still essential to the model and the default values are put in keeping in mind the most standard practices and use cases

5. `channels`: Number of channels of the image that should be fed into the network. 1 for `grayscale`, 3 for `rbg` and 4 for `rgba` . Default = `3`.

6. `use-pretrained`: Boolen variable which decided if a pre-trained version of the ResNet50 model should be used. If set to `False`, the model trains from scratch. Default = `True`.

7. `output-path`: Path to the location where the user wants to save the output metrics, the model. Default = `.`

8. `batch-size`: Batch size that the `ImageDataGenerator` generates and feeds to the network. This affects the number of steps per epoch also. **Note**: No part of your training or validation set should be smaller than the `batch-size` as this will return 
an error.  Default = `32`.

9. validation-split (float): Fraction of the actual dataset which should be used for validation. Default = `0.25`.

10. class_mode (str): Mode of the classes that the experiment aims to solve. Possible values: "categorical", "binary", "sparse", "input", or None. Default = `categorical`.

11. learning-rate (float): Learning rate of the Adam Optimizer. Default = `0.0001`.

12. loss (str): loss function used to compile model. Default = `categorical_crossentropy`.


# Executing the Model scripts
    
## Resnet50

    python resnet50.py --images-path ../../PATH_TO_DATA --output-path ../../PATH_TO_OUTPUT --height 100 --width 100 --channels 3 --use_pretrained False --epochs 35 --batch-size 32 --validation-split .35 --loss binary_crossentropy --learning-rate 0.002 
    
### Outputs 

1. Model weights: model weights are saved in .h5 format which can be used for later use. They are saved as model_Resnet50_{timestamp}_epochs_{number of epocs}.h5
2. Figures of metrics: Two plots showing graphical distribution of accuracy vs validation accuracy and loss vs validation loss. They are saved as fig1.png and fig2.png
3. Json dumps of metrics: Two different json dumps.
    1. experiment_batch.json: Showing accuracy and loss as calculated at the end of each batch. Output frequency is too high to be used for graphical represnetation. Closest to realtime
    2. experiment.json: Showing acccuracy, loss, validation accuracy and validation loss as calculated at the end of each epoch. This is the file to be parsed for grapphical representation.

Format of experiment.json:
    
        {
            "epoch_number":
            {
                "acc": Accuracy at end of epoch,
                "val_acc": Validation Accuracy at end of epoch,
                "loss": Loss at end of epoch,
                "val_acc": Validation Loss at end of epoch,
            }
        }

Example:

        {
            "0": 
            {
                "acc": 0.48484848484848486,
                "val_acc": 0.5,
                "loss": 7.721049770911451,
                "val_loss": 8.059047736904837
            }
        }
        
> Info: All the ouput files will be found in the directory specified by `--output-path`.


