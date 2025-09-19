# ECE BOARD EXAM PROBLEM

This project analyzes student performance data using innovative data wrangling and visualization techniques. Data wrangling involves cleaning and filtering the dataset to create specific DataFrames that focus on particular student groups based on predetermined criteria. Following this, data visualization is utilized to visually represent the findings, which aids in comparing performance across different tracks, genders, and hometowns.

# 1. Data Frames
By applying certain parameters and choosing specific columns, the process entails generating individual DataFrames from the dataset. For instance, one DataFrame should filter instrumentation students from Luzon with Electronics grades above 70. The choice of 'instrumentation students' and 'Luzon' as parameters, and 'Electronics grades' as a column, is significant as it allows us to focus on a specific group and their performance. A different DataFrame should be used to filter out Mindanao female students with calculated average grades of at least 55, which again, is a specific group chosen for analysis based on the parameters of 'Mindanao', 'female students', and 'average grades'. 

	import pandas as pd

	# Load dataset
	df = pd.read_excel('board2.xlsx')


	# (a) Instru DataFrame

	# Filter rows
 
	Instru = df.loc[
    (df['Track'] == 'Instrumentation') &
    (df['Hometown'] == 'Luzon') &
    (df['Electronics'] > 70),
    ['Name', 'GEAS', 'Electronics']
	]

	display(Instru)


	# (b) Mindy DataFrame

	# Create Average column
 
	df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

	# Filter rows
 
	Mindy = df.loc[
    (df['Hometown'] == 'Mindanao') &
    (df['Gender'] == 'Female') &
    (df['Average'] >= 55),
    ['Name', 'Track', 'Electronics', 'Average']
	]

	# Display result
 
	display(Mindy)


# 2. Visualization
To analyze how factors such as track, gender, and hometown influence students' overall average grades, this assignment requires the creation of visualizations. These graphs bring clarity to the patterns or variations in the performance of different groups, making comparisons more straightforward and the task less daunting.

	import matplotlib.pyplot as plt   # Import matplotlib for plotting


	# Compute group averages

	# Group the dataset by 'Track' and compute the mean of the 'Average' column
	avg_track = df.groupby('Track')['Average'].mean()

	# Group the dataset by 'Gender' and compute the mean of the 'Average' column
	avg_gender = df.groupby('Gender')['Average'].mean()

	# Group the dataset by 'Hometown' and compute the mean of the 'Average' column
	avg_hometown = df.groupby('Hometown')['Average'].mean()



	# Prepare the figure

	plt.figure(figsize=(12, 6))  # Set figure size to fit 3 subplots side by side



	# Plot Average by Track

	plt.subplot(1, 3, 1)                            # First subplot (1 row, 3 cols, position 1)
	plt.bar(avg_track.index, avg_track.values)      # Bar chart: x = Track names, y = average scores
	plt.xticks(rotation=45)                         # Rotate x-labels for readability
	plt.title("Average by Track")                   # Add chart title
	plt.ylabel("Average Grade")                     # Label y-axis



	# Plot Average by Gender

	plt.subplot(1, 3, 2)                            # Second subplot (position 2)
	plt.bar(avg_gender.index, avg_gender.values)    # Bar chart for Gender
	plt.title("Average by Gender")                  # Add chart title



	# Plot Average by Hometown

	plt.subplot(1, 3, 3)                            # Third subplot (position 3)
	plt.bar(avg_hometown.index, avg_hometown.values) # Bar chart for Hometown
	plt.title("Average by Hometown")                 # Add chart title



	# Final adjustments

	plt.tight_layout()   # Adjust spacing so plots don’t overlap
	plt.show()           # Display all 3 charts together

The evaluations highlighted the importance of data manipulation and visualization in analyzing student performance. Filtering techniques were employed to isolate and examine specific student groups based on criteria. The visualizations facilitated easy comparisons of average grades across different tracks, genders, and hometowns. Together, these methods demonstrated that graphical representation and well-organized data manipulation can provide valuable insights into educational achievement, motivating us to continue our work.
