# OCR Table Extraction with Nanonets-OCR-s

This Jupyter notebook demonstrates how to perform Optical Character Recognition (OCR) on an image containing a table and extract its content, specifically focusing on converting the table into HTML format. It leverages the `nanonets/Nanonets-OCR-s` model from the Hugging Face Transformers library.

## Features

-   **Table Extraction:** Accurately extracts tabular data from images.
-   **HTML Output:** Converts extracted tables into well-formatted HTML table structures.
-   **LaTeX for Equations:** Designed to return equations in LaTeX representation (though not explicitly shown in the provided example, the prompt includes this functionality).
-   **Image Description/Captioning:** Includes logic to add descriptions or captions for images within `<img>` tags.
-   **Watermark and Page Number Handling:** Wraps watermarks and page numbers in special bracketed tags for easy identification.
-   **Checkbox Support:** Prefers using `☐` and `☑` for checkboxes.

## Setup

### Prerequisites

Before running the notebook, ensure you have Python installed and access to a Jupyter environment (e.g., Jupyter Lab, Jupyter Notebook, or Google Colab).

### Installation

Install the necessary Python libraries using pip:

```bash
pip install Pillow "transformers[torch]"
```

## Usage

1.  **Upload your image:** Place the image file you want to process (e.g., `Excel-table-inserted-in-Worksheet.png`) in a location accessible by the notebook. If running in Kaggle, you might upload it as a dataset.

2.  **Specify `image_path`:** In the notebook, update the `image_path` variable to point to your image file:

    ```python
    image_path = "/path/to/your/image.png" # Example: "/kaggle/input/tableexcel/Excel-table-inserted-in-Worksheet.png"
    ```

3.  **Run the cells:** Execute all cells in the notebook sequentially.

    -   The first cell installs the required libraries.
    -   The second cell imports necessary modules.
    -   The third cell loads the `nanonets/Nanonets-OCR-s` model and processor, then defines the `ocr_page_with_nanonets_s` function which performs the OCR and formatting.
    -   The final cell calls the OCR function and prints the result.
    -   The last cell saves the OCR result to a file (e.g., `my_document_output.txt`).

### Example Output (HTML Table)

The notebook will output the extracted table content in HTML format, similar to this:

```html
<table>
  <tr>
    <td>A</td>
    <td>B</td>
    <td>C</td>
    <td>D</td>
    <td>E</td>
    <td>F</td>
  </tr>
  <tr>
    <td><strong>Store</strong></td>
    <td><strong>Region</strong></td>
    <td><strong>Q1</strong></td>
    <td><strong>Q2</strong></td>
    <td><strong>Q3</strong></td>
    <td><strong>Q4</strong></td>
  </tr>
  <!-- ... more rows ... -->
</table>
```

## Function Details

### `ocr_page_with_nanonets_s(image_path, model, processor, max_new_tokens=4096)`

This function takes an image path, the loaded model, and processor, and an optional `max_new_tokens` argument to control the maximum length of the generated output.

-   **`image_path`**: Path to the input image file.
-   **`model`**: The loaded `AutoModelForImageTextToText` instance.
-   **`processor`**: The loaded `AutoProcessor` instance.
-   **`max_new_tokens`**: (Optional) Maximum number of new tokens to generate in the output. Default is 4096.

The function constructs a detailed prompt for the model, including instructions for table formatting, LaTeX for equations, image handling, watermarks, and page numbers. It then processes the image and prompt, generates the OCR output, and decodes it.

### `save_ocr_result_to_file(result_string: str, filename: str, file_format: str = "txt")`

This utility function saves the OCR result string to a specified file.

-   **`result_string`**: The string content to be saved.
-   **`filename`**: The base name for the output file (e.g., "my_document_output").
-   **`file_format`**: (Optional) The format of the file, either "txt" or "md". Defaults to "txt".

## Model Information

The notebook uses the `nanonets/Nanonets-OCR-s` model, which is a powerful OCR model available on Hugging Face. You can find more details about it [here](https://huggingface.co/nanonets/Nanonets-OCR-s).

## License

(Consider adding a license if you plan to share this publicly, e.g., MIT, Apache 2.0)
