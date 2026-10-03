# DigitLab — AI Handwritten Digit Recognition

An internship project with a drawing studio, live model predictions, top\-three scores, a pixel preview, dataset examples, and an evaluation dashboard\. Uses a real trained logistic\-regression model\. Predictions run locally in your browser; no API key is required\.

## Run

Unzip the project and open **index\.html** in a modern browser\. Draw one large digit from 0 to 9, then click **Recognize digit**\. You can also load a dataset sample and recognize it\. **Clear canvas** resets the drawing and result\.

Optional local server with Node\.js 18 or later:

```sh
npm start
```

Open the localhost URL printed by the server\. No npm install is required\.

## Measured results

- Dataset: scikit\-learn Digits, 1,797 grayscale 8×8 images, ten classes\.
- Training: 1,437 images; test: 360 images\.
- Stratified 80/20 split, random seed 42\.
- StandardScaler fitted on training images only\.
- LogisticRegression&#40;C=1, max\_iter=2000, random\_state=42&#41;\.
- Test accuracy: 350 / 360 = **97\.22%**\. Macro F1: **0\.97194**\.

`evaluation.json` contains the full measured report and confusion matrix\. This score is for the held\-out dataset; accuracy on new browser drawings has not been quantified\. Model scores are not calibrated guarantees\. Poorly centered digits, different stroke styles, letters, multiple digits and scribbles can produce incorrect predictions with high scores\.

## Reproduce training

Python 3\.11 or later is required for the pinned scikit\-learn version\.

```sh
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
python train_model.py
```

This regenerates model\.js and evaluation\.json\. Coefficients incorporate the fitted scaler so browser inference matches the Python pipeline\. Canvas drawings are cropped, centered, resized and reduced to 64 grayscale values\. Dataset samples use their original pixel values\. A sample gallery provides one first\-selected test example per class\.

## Check the model

```sh
npm test
python tests/check_parity.py
```

The parity check compares JavaScript predictions and probabilities against the Python pipeline on all 360 held\-out inputs\.

## GitHub and GitHub Pages

Create a GitHub repository and upload the **contents** of this folder, including index\.html, style\.css, app\.js, inference\.js and model\.js\. Do not upload only the ZIP\. In repository Settings → Pages choose Deploy from a branch, main, and / &#40;root&#41;\. Save and use the URL GitHub provides\. The app is fully static\.

## Files

- index\.html, style\.css, app\.js: interface and drawing preprocessing\.
- inference\.js: reusable JavaScript classifier\.
- model\.js: exported trained coefficients, metrics and sample images\.
- train\_model\.py: reproducible model training\.
- evaluation\.json: evaluation evidence\.
- tests/: input validation and Python/JavaScript parity checks\.
- screenshots/: genuine browser captures\.

## References

- [scikit\-learn Digits dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_digits.html)
- [LogisticRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)
- [GitHub Pages publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

Educational prototype\. No drawing is uploaded or stored by the app\. Report internship dates and contributions should reflect your actual work\.
