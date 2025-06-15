## Bayesian Optimization Competition Report

### Overview

This report documents the evolution of the codebase developed for the Bayesian Optimization competition, focusing on the challenges encountered, strategies implemented, and lessons learned throughout the process. The goal was to optimize a black-box functions, leveraging Gaussian Processes (GP) and various acquisition functions to efficiently explore the input space.   The competition involved optimizing a set of functions with varying characteristics.

### Initial codebase

The initial codebase was taken from the **Required activity 12.2: Jupyter Notebook on Bayesian optimisation**. The structure and approach were inspired by common Bayesian optimization workflows, with code adapted from Jupyter Notebook on Bayesian optimisation, documentation for Gaussian Processes and acquisition functions. The decision to use this code as a starting point was based on the knowledge gained from Module 12, its flexibility, extensibility, and proven effectiveness for black-box optimization tasks, as was described in the competition brief. The codebase was designed to be flexible and extensible, allowing for rapid experimentation with different strategies and configurations. 

**NOTE:** Jupyter notebooks for each function are available in directories named **function_1, function_2, function_3, function_4, function_5, function_6, function_7 and function_8**

### Code modification

I started with GaussianProcessRegressor with default kernel and one acquisition function (UCB). This did only work for Function 1, 2 and Function 8, for functions 3-7, I had to implement additional strategies as below. Throughout the competition, the codebase evolved in several key ways:

- **Data Handling Improvements:** Functions were added to load and preprocess additional queries and observations from external files, ensuring the dataset remained up-to-date and comprehensive.
- **Significant Observation Extraction:** A function was introduced to identify and focus on significant observations, allowing for targeted exploitation around those points.
- **Visualization Enhancements:** 2D and 3D scatter plots were implemented to better understand the spatial distribution of the data and guide further exploration.
- **Acquisition Function Expansion:** Multiple acquisition functions (UCB, PI, EI, Thompson Sampling) were implemented and parameterized, enabling experimentation with different exploration-exploitation strategies.
- **Grid Sampling Strategies:** Separate functions for exploration and exploitation grids including Latin Hypercube were developed to efficiently sample the input space both globally and locally.
- **Hyperparameter Optimization:** Integration with `scikit-optimize` (`gp_minimize`) and `bayes_opt` (`BayesianOptimization`) allowed for automated tuning of kernel types, lengthscales, noise assumptions, and acquisition function parameters.
- **Kernel Flexibility:** Support for multiple kernel types (RBF, Matern, RationalQuadratic, DotProduct) was added, improving model adaptability to the underlying data structure.

Most modifications were driven by feedback from the programme via observations, and best practices learned from literature. Notably, the introduction of hyperparameter optimization and the use of multiple acquisition functions led to measurable improvements in the score.

### Final result

In the final weeks, the score improved as the code leveraged optimized hyperparameters and more sophisticated acquisition strategies. The ability to exploit around significant observations and adapt the kernel to the data proved particularly effective. If more weeks were available, further improvements could include ensembling multiple GP models, incorporating domain-specific priors, or using active learning strategies to select queries.

Key learnings from the competition include the importance of flexible model design, the value of automated hyperparameter tuning, and the need for robust data handling. For future competitions, I would start with a more modular codebase, automate more of the experimentation process, and invest earlier in visualization and diagnostics. If starting over, I would also prioritize integrating advanced acquisition functions and kernel selection from the outset.

### Reflections and Lessons Learned

#### Challenges Encountered

Throughout the competition, several challenges emerged across all eight functions, each with unique characteristics that shaped the evolution of the codebase and my understanding of Bayesian optimization in practice:

- **Sparse and Noisy Observations:** For most functions (notably Functions 2–7), the majority of observations were zero or near-zero except in the immediate vicinity of a contamination source. This made it difficult for the Gaussian Process (GP) to learn a meaningful model from the initial data, especially for functions with weaker or more subtle sources. Function 1 and Function 8, with more pronounced signals, were easier to model, but the code had to be adapted to focus on identifying and exploiting rare, significant observations for the others.
- **Multiple Modes and Local Optima:** Several functions (e.g., Functions 3, 5, and 7) exhibited complex landscapes, leading to multi-modal optimization problems. Early versions of the code tended to exploit the first detected source, neglecting others. This highlighted the need for robust exploration strategies and the importance of acquisition functions that balance exploration and exploitation.
- **Kernel Selection and Hyperparameter Sensitivity:** The default RBF kernel worked well for some functions (notably Functions 1, 2 and 8) but failed for others, particularly when the underlying function was less smooth or had abrupt changes (as in Functions 4 and 6). Tuning kernel parameters and experimenting with alternative kernels (Matern, RationalQuadratic, DotProduct) became essential. Automated hyperparameter optimization with `gp_minimize` and `BayesianOptimization` proved invaluable, but also introduced computational overhead and required careful management of search spaces and parameter bounds.
- **Computational Efficiency:** As the dataset grew and more sophisticated models were used, computational demands increased, especially during grid search and hyperparameter optimization. This was particularly evident for Functions 3–7, where more complex models and finer grids were needed. Efficient data handling, vectorized operations, and judicious use of grid resolution were necessary to keep runtimes manageable.
- **Integration of External Data:** Incorporating additional queries and observations from external files required robust data loading and preprocessing routines. Ensuring consistency between input and output arrays, handling missing or malformed data, and updating the dataset dynamically were all non-trivial tasks that required careful attention, especially as the number of functions and queries increased.

#### Strategies for Overcoming Challenges

To address these challenges across all functions, several strategies were implemented:

- **Flexible Acquisition Functions:** Implementing multiple acquisition functions (UCB, PI, EI, Thompson Sampling) and allowing for parameterization enabled experimentation with different exploration-exploitation trade-offs. This flexibility was crucial for adapting to the characteristics of each function and for discovering both sources in multi-modal landscapes.
- **Grid Sampling and Adaptive Resolution:** Separate functions for global exploration and local exploitation grids allowed the code to efficiently sample the input space at different resolutions. This hierarchical approach facilitated broad searches when little was known and focused searches when promising regions were identified, which was particularly useful for functions with multiple or subtle sources.
- **Automated Hyperparameter Optimization:** Integrating `scikit-optimize` and `bayes_opt` for hyperparameter tuning automated the process of finding optimal kernel types, lengthscales, noise assumptions, and acquisition function parameters. This not only improved model performance but also provided insights into which configurations worked best for different types of functions.
- **Visualization and Diagnostics:** Implementing 2D and 3D scatter plots of the input and output data provided valuable intuition about the spatial distribution of observations and the effectiveness of the search strategy. Visual diagnostics helped identify issues such as overfitting, underfitting, or missed sources, and guided further code modifications.

#### Impact of Code Modifications

Each modification to the codebase was motivated by a specific challenge or opportunity for improvement, often revealed by the behavior of different functions:

- **Data Handling Improvements:** Ensured that the dataset remained comprehensive and up-to-date, enabling the model to learn from all available information across all functions.
- **Visualization Enhancements:** Provided intuitive feedback on model performance and guided further exploration, revealing differences in function landscapes.
- **Acquisition Function Expansion:** Enabled experimentation with different strategies, improving the robustness of the search and allowing adaptation to the unique challenges of each function.
- **Grid Sampling Strategies:** Balanced the need for global exploration and local exploitation, increasing the efficiency of the search, particularly for functions with multiple sources.
- **Hyperparameter Optimization:** Automated the process of finding optimal model configurations, leading to measurable improvements in performance across the diverse set of functions.
- **Kernel Flexibility:** Improved the model's ability to adapt to different underlying data structures, increasing its generality and effectiveness.

#### Results and Performance

The cumulative effect of these modifications was a steady improvement in the competition score across all eight functions. Early versions of the code struggled to find both sources or to adapt to functions with different characteristics. As the codebase evolved, the combination of automated hyperparameter tuning, flexible acquisition functions, and targeted exploitation led to more consistent and higher scores.

In particular, the ability to exploit around significant observations and to adapt the kernel to the data proved especially effective. Automated hyperparameter optimization often identified non-intuitive configurations that outperformed manual tuning, highlighting the value of systematic experimentation. Functions 1, 2 and 8 benefited from simpler models, while Functions 3–7 required more sophisticated strategies and parameter tuning.

#### Potential Future Improvements

Given more time, several avenues for further improvement could be explored for all functions:

- **Model Ensembling:** Combining predictions from multiple GP models with different kernels or hyperparameters could improve robustness and performance, especially in multi-modal or noisy settings.
- **Active Learning Strategies:** Implementing more sophisticated query selection strategies, such as batch acquisition could further enhance the efficiency of the search.
- **Automated Experimentation:** Developing a more modular and automated experimentation framework would facilitate rapid testing of different configurations and strategies.
- **Advanced Acquisition Functions:** Exploring state-of-the-art acquisition functions, such as entropy search or knowledge gradient, could provide additional performance gains.
- **Parallelization and Scalability:** Optimizing the code for parallel execution and scalability would enable more extensive searches and faster experimentation.

#### Key Learnings

The competition provided valuable insights into both the theory and practice of Bayesian optimization across a diverse set of functions:

- **Flexibility is Crucial:** A flexible and extensible codebase is essential for adapting to new challenges and for experimenting with different strategies.
- **Automated Tuning Pays Off:** Automated hyperparameter optimization can uncover effective configurations that may not be obvious through manual tuning, especially when dealing with diverse function landscapes.
- **Data Handling Matters:** Robust data loading, preprocessing, and management are foundational to effective modeling and experimentation.
- **Visualization Guides Development:** Visual diagnostics are invaluable for understanding model behavior and for identifying areas for improvement.
- **Exploration-Exploitation Balance:** Balancing exploration and exploitation is a central challenge in Bayesian optimization, and flexible acquisition functions are key to achieving this balance.
- **Kernel Selection is Non-Trivial:** The choice of kernel and its parameters can have a profound impact on model performance, especially in complex or noisy settings.

#### Recommendations for Future Work

For future competitions or similar projects, I would recommend the following:

- **Start with a Modular Codebase:** Design the code to be modular and extensible from the outset, facilitating rapid experimentation and adaptation.
- **Automate Experimentation Early:** Invest in automation for hyperparameter tuning, model selection, and diagnostics to accelerate the development process.
- **Prioritize Visualization:** Implement visualization tools early to guide development and to provide intuitive feedback on model performance.
- **Explore Advanced Methods:** Stay abreast of advances in Bayesian optimization, including new acquisition functions, model types, and active learning strategies.
- **Document and Reflect:** Maintain thorough documentation of code modifications, experimental results, and lessons learned to inform future work.

#### Conclusion

Participating in this competition was a valuable learning experience that deepened my understanding of Bayesian optimization, Gaussian Processes, and black-box function optimization. The iterative process of identifying challenges, implementing solutions, and reflecting on results led to a robust and flexible codebase capable of tackling a range of optimization problems.

The key to success was a willingness to experiment, to learn from both successes and failures, and to continually refine the approach based on feedback and new insights. The lessons learned will inform future work in Bayesian optimization and related fields, and the codebase developed during the competition provides a strong foundation for further exploration and innovation across a variety of function types.
