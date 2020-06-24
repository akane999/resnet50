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
