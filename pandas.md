import pandas as pd

# create dataframe
my_df = pd.DataFrame(columns=["column 1", "column 2"])

# create and fill a dataframe
another_df = pd.DataFrame({
    "column 1": ["value", "value", "value"],
    "column 2": ["value of column 2", "another value of column 2", "test"]
})

# look at its shape
print(another_df.shape)

# Display the data types of each column
print(df.dtypes)

# drop first (or any other row) of a dataframe
# also resetting index and dropping the old one
# (otherwise it will show up as a column)
another_df.drop(another_df.index[0], inplace=True)
another_df.reset_index(drop=True, inplace=True)

# turn a list into a dataframe
my_list = ["one", "two", "three"]
my_dataframe = pd.DataFrame(my_list, columns=["numbers"])

# turning a dictionary into a dataframe
my_dict = {"tree": "green",
            "table": "brown",
            "computer": "black",
            "test": None}
df_colors = pd.DataFrame.from_dict(my_dict, orient="index", columns=["color"])
# resetting index so the dictionary key is not the index but another column
df_colors = df_colors.reset_index()
df_colors = df_colors.rename(columns={"index": "object"})

# change the value of a particular cell
df_colors.loc[df_colors["object"] == "tree", "color"] = "brown and green"

# read a csv file as a df
df = pd.read_csv("nameorlink.csv", sep=",")

# turn a df into a csv file
df.to_csv("nameofmydf.csv", sep=",", encoding="utf-8", index=False)

# check if a particular value is in a particular column of a df
if "computer" in df_colors["object"].values:
    print("Yes, you choose the name of the df, then the column you want to look through and end in .values")
else:
    "nope"

# merge two dataframes that share a column (if column name is the same in both dataframes)
df_merged = pd.merge(df_one, df_two, on="shared_column")

# if column names are different -> will keep both columns, one will have to be deleted after the merge
df_merged = pd.merge(df_one, df_two, left_on="left_column", right_on="right_column")

# Rename the column 'old_name' to 'new_name'
df.rename(columns={'old_name': 'new_name'}, inplace=True)

# Drop rows where 'deaths' column has None values
df.dropna(subset=['deaths'], inplace=True)

# check for missing values
missing_values = df_colors[df_colors.isna().any(axis=1)]
print(f"1 way to check: {missing_values}")
print()

missing_values = df_colors.isna().sum()
print(f"2 way to check: {missing_values}")
print()

print("3 way to check:")
for column in df_colors.columns:
    if df_colors[column].isna().any():
        print(f"{column} has missing values")

# change the value of a particular cell
candidatures.loc[candidatures["status"] == "non retenue", "status"] = "refus"
df_colors.loc[df_colors["object"] == "tree", "color"] = "brown and green"

