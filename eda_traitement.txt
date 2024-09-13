import pandas as pd

# display first rows
print(df.head())

# look at datatypes
print(df.dtypes)

# describe dataset
print(df.describe())

# check for missing values
for column in df.columns:
    if df[column].isna().any():
        print(f"{column} has {df[column].isna().sum()} missing values")

# check for duplicates, using keep=False will display all the duplicates (not just one instance of it)
print(f"There are {df.duplicated().sum()} duplicates")
duplicate_rows = df[df.duplicated(keep=False)]

# drop duplicates, in this case keeping the first instance of it
df.drop_duplicates(keep="first", inplace=True)

"""missing values"""

# drop missing values (all or from a particular column)
# reset index so it's continuous
df.dropna(inplace=True)
df.dropna(subset=["column"], inplace=True)
df.reset_index(drop=True, inplace=True)

# methods to fill missing values of a particular column

# median
median_df_column = df.loc[:,"column"].median()
df["column"].fillna(median_df_column, inplace=True)

# mean
mean_df_column = df.loc[:,"column"].mean()
df["column"].fillna(mean_df_column, inplace = True)

# last valid observation: forward fill (ffill)
df["column"].fillna(method = "ffill", inplace = True)

# next valid observation: backward fill (bfill)
df["column"].fillna(method="bfill", inplace=True)

# assigning custom value to a variable
new_df_column = "unknown"
df["column"].fillna(new_df_column, inplace = True)


"""turn categorical values into numerical values"""

# factorize to turn categories into numerical values
df["sex"] = df["sex"].factorize()[0]

# get dummies
df = pd.concat([df, df["embark_town"].str.get_dummies()], axis=1)


"""standardization (especially for classification KNN and logistic regression)"""

from sklearn.preprocessing import StandardScaler

X = df_zoom[["age", "income"]]
y = df_zoom["purchases"]

X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=2)

scaler = StandardScaler().fit(X_train)

X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)


"""PCA"""
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
X_pca = pca.fit_transform(X)
