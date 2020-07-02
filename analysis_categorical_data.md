#Melt by category_list to remove rows with value 1


sectors_melted = pd.melt(sectors, id_vars=['category_list'], var_name ='main_sector')