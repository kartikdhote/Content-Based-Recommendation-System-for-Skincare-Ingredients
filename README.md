# Cosmetic Ingredient Similarity Mapping & Recommendation System (t‑SNE, Bokeh)

Problem Statement:
Buying skincare is confusing for customers with dry or sensitive skin because ingredient lists are long and technical.
This project analyzes cosmetic ingredient lists and builds an interactive similarity map so users and businesses can quickly find products with similar formulations, especially moisturizers for dry skin.

Tools & Technologies:
Programming: Python
Libraries: pandas, NumPy, scikit‑learn (t‑SNE), Bokeh
Environment: Jupyter Notebook
Data Format: CSV (cosmetics dataset)

Dataset Description
Source: Cosmetics product dataset provided by MedTourEasy during traineeship.

Size: 1,000+ cosmetic products across multiple categories (moisturizers, cleansers, etc.).
Key columns (used in this project):
Name – Product name
Brand – Brand name
Label – Product category (e.g., “Moisturizer”)
Dry – Binary flag indicating suitability for dry skin
Ingredients – Full ingredient list as a comma‑separated string
Price, Rank – Basic business metadata
This project filters the dataset down to moisturizers suitable for dry skin and works only on that subset.


Key Steps in Analysis:

1) Data Loading & Filtering
    Load the CSV file using pandas.read_csv.
    Filter records where Label == "Moisturizer" and Dry == 1.
    Reset index and keep only relevant columns for analysis and visualization.
2) Ingredient Text Processing
    Convert ingredient strings to lowercase.
    Split on commas to create a token list per product.
    Build a vocabulary: a dictionary mapping each unique ingredient to a numeric index.
3) One‑Hot Encoding (Document–Term Matrix)
    Initialize a matrix of shape (num_products, num_unique_ingredients).
    For each product, mark 1 where an ingredient is present and 0 otherwise.
    This matrix is the high‑dimensional numerical representation of product formulations.
4) Dimensionality Reduction with t‑SNE
    Apply TSNE(n_components=2, learning_rate=200, random_state=42) on the matrix.
    Generate 2D coordinates (X, Y) for each product while preserving local similarity structure.
5) Interactive Visualization with Bokeh
    Create a ColumnDataSource from the filtered DataFrame.
    Build a 2D scatter plot where each point is a product (X vs Y).
    Add a HoverTool to show: Name, Brand, Price, Rank on mouse‑over.
    Render in notebook for interactive exploration.
6) Qualitative Validation
    Select example products (e.g., “Color Control Cushion…” vs “BB Cushion Hydra Radiance…”).
    Compare their ingredient lists to confirm that nearby points share similar ingredients.

Key Insights / Results
*Products that appear close together on the t‑SNE scatter plot have significant overlap in ingredients, indicating similar formulations.
*The map highlights clusters of moisturizers that likely behave similarly on dry skin (e.g., high in humectants, occlusives, or certain UV filters).
*The pipeline can be extended into a content‑based recommendation engine: recommend products that are near a user’s preferred (or avoided) product in the embedding space.

