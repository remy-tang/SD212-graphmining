# SD212 project - Graph mining

The goal of this project is to find how to compensate the most common nutrient deficiencies in vegetarian diets.

According to this scientific article [Nutrition concerns and health effects of vegetarian diets (Craig WJ 2010)](https://pubmed.ncbi.nlm.nih.gov/21139125/), the most common nutrient deficiencies in vegetarian diets involve "vitamin B12, vitamin D, ω-3 fatty acids, calcium, iron, and zinc". 

On the contrary, such a diet provides plenty of fiber, vitamin C, and β-carotene (a precusor of vitamin A found in fruits and vegetables). Our dataset does not provide ω-3 fatty acids and calcium content of the food, so we will only study the other nutrients. Side note : vitamin D increases calcium absorption in the body, so it is not completely unrelated to calcium availability.

More specifically, we want to build food groups from nutritional information of common foods, based on their nutrient profile (for a few select nutrients). All the foods in a group should have a similar nutrient availability.
This way, we will try to identify fruits and vegetables (by their high fiber, vitamin C, and β-carotene content) that have either high vitamin B12, calcium, iron, zinc, or a combination of them.

## Dataset information & preprocessing

The dataset was collected from Kaggle. More specifically, the Kaggle dataset contains food nutrient availability for 7413 foods, pertaining to 1183 unique categories (e.g. cheese, egg, vegetable oil, etc.).

The Kaggle dataset itself was extracted from the U.S. Department of Agriculture, and contains the "most common" foods from the complete dataset. However, when exploring the data, we discovered that there were many uncommon items (for example Alaskan whale meat, which belongs in the `WHALE` category). We still chose to keep all foods to avoid doing unecessary work.

To build the adjacency matrix from this data, we first decided to select a few key nutrients to build a 'nutrient vector'. This allowed us to easily compare food in the space of the selected nutrients.

We also normalized all nutrients to make more relevant comparisons between nutrient quantities, as we did not search for their nominal values.

Then we chose to make links between two instances of food if the distance between their nutrient vector was smaller than a certain hand-tuned threshold.

A lot of iterations were necessary in order to tune the number of selected nutrients, as well as the distance threshold to get a satisfying result. This process was therefore very time-consuming as we did not find any other way to create relevant edges.

The selected nutrients are Vit. B12, Calcium, Iron, Zinc, Fiber, Vit. C, Beta-Caroteme. The threshold was tuned to that the number of edges be around $10^5$ to $10^6$, so that we respect the constraints imposed by the project rules while still keeping a good amount of edges.

