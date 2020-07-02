READING FILES
 f = open("my_file.txt","r")
file_as_string = f.read()
# Open the file my_file.txt and assign its contents to s

import csv
f = open("my_dataset.csv","r")
csvreader = csv.reader(f)
csv_as_list = list(csvreader)
# Open the CSV file my_dataset.csv and assign its data to the list of lists csv_as_list

#Right join of Companies and Rounds to understand extra companies in Rounds
master_frame = pd.merge(companies, rounds, how='right', left_on='permalink', right_on='company_permalink')


master_frame = pd.merge(master_frame, sectors, how='inner', left_on='primary_sector',right_on='category_list')

