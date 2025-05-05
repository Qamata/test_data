# test_data
50 Handwritten digits to be used to test validate a number image recognition model

# Loading the Handwritten Digits Dataset

This README provides instructions on how to load the handwritten digits dataset stored as a pickled file (`digits_shuffled.pkl`) from a GitHub repository. This dataset contains images of digits (0-9) that have been processed and are ready for use in machine learning models, particularly for MNIST-like tasks.

## Prerequisites

* **Python 3.x** installed on your system.
* The following Python libraries:
    * `requests`: For fetching data from URLs. You can install it using pip:
        ```bash
        pip install requests
        ```
    * `pickle`: This is a built-in Python module, so you don't need to install it separately.
    * `numpy`: For numerical operations and handling the image data as arrays. You can install it using pip:
        ```bash
        pip install numpy
        ```

## Loading Instructions

Follow these steps to load the dataset into your Python environment:

1.  **Get the Raw URL of the `.pkl` File:**
    * Navigate to the location of the `digits_shuffled.pkl` file in the GitHub repository where it is stored.
    * Click on the filename to view its contents (which will likely appear as gibberish since it's a binary file).
    * Look for the "Raw" button (usually on the right side of the file view).
    * Click the "Raw" button. This will open the raw binary content of the file in your browser.
    * **Copy the URL** from the address bar of your browser. This is the raw URL you will use in the Python script. It should look something like:
        ```
        [https://raw.githubusercontent.com/your_username/your_repository/main/path/to/digits_shuffled.pkl](https://raw.githubusercontent.com/your_username/your_repository/main/path/to/digits_shuffled.pkl)
        ```
        **Make sure it starts with `https://raw.githubusercontent.com/`.**

2.  **Use the Following Python Code to Load the Data:**

    ```python
    import requests
    import pickle
    import numpy as np
    from io import BytesIO

    # Replace with the raw URL of your .pkl file on GitHub
    pkl_url = "YOUR_RAW_GITHUB_PKL_URL_HERE"

    try:
        response = requests.get(pkl_url)
        response.raise_for_status()  # Raise an exception for bad status codes

        # Load the pickled data from the response content
        loaded_data = pickle.load(BytesIO(response.content))

        # Assuming the .pkl file contains a tuple of (X, y)
        loaded_X, loaded_y = loaded_data

        print("Shape of loaded image data (loaded_X):", loaded_X.shape)
        print("Shape of loaded labels (loaded_y):", loaded_y.shape)
        print("Example loaded image (first in the dataset):\n", loaded_X[0])
        print("Example loaded label (first in the dataset):", loaded_y[0])

        # Now you can use 'loaded_X' as your image data and 'loaded_y' as your labels
        # for training or evaluating your machine learning model.

    except requests.exceptions.RequestException as e:
        print(f"Error downloading the .pkl file: {e}")
    except pickle.PickleError as e:
        print(f"Error unpickling the data: {e}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")
    ```

3.  **Replace Placeholder URL:** Make sure to replace `"YOUR_RAW_GITHUB_PKL_URL_HERE"` in the Python code with the actual raw URL you copied in step 1.

4.  **Run the Script:** Execute the Python script. If the URL is correct and the network connection is stable, the script will download the `.pkl` file, load the data, and print the shapes of the loaded image data and labels, along with an example.

## Data Format

The loaded data will be a tuple containing two NumPy arrays:

* **`loaded_X`:** This array contains the image data. Each image is likely a 28x28 pixel grayscale image, flattened into a 1D array or stored as a 2D array, depending on how it was processed before pickling. Check the `shape` of `loaded_X` to determine its exact structure.
* **`loaded_y`:** This array contains the corresponding labels for each image in `loaded_X`. The labels will be integers from 0 to 9, representing the digit depicted in the image.

## Usage

After successfully loading the data, you can use `loaded_X` and `loaded_y` to train or evaluate your handwritten digit recognition models. Ensure that your model's input layer is compatible with the shape of the images in `loaded_X`.

## Troubleshooting

* **Incorrect Raw URL:** Double-check that you have copied the **raw** URL of the `.pkl` file from GitHub. The URL should start with `https://raw.githubusercontent.com/`.
* **Network Issues:** Ensure you have a stable internet connection to download the file.
* **File Not Found (404 Error):** Verify that the `.pkl` file exists at the specified path in your GitHub repository and that the URL is correctly typed.
* **Pickle Errors:** If you encounter `pickle.PickleError`, it might indicate that the file is corrupted or was created with a different version of Python's `pickle` module. Ensure the file was uploaded correctly and try loading it with the same Python version used for saving.

By following these instructions, you should be able to easily load the handwritten digits dataset from the provided GitHub URL.
