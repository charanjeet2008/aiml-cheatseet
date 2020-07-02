#Right join of Companies and Rounds to understand extra companies in Rounds
master_frame = pd.merge(companies, rounds, how='right', left_on='permalink', right_on='company_permalink')


master_frame = pd.merge(master_frame, sectors, how='inner', left_on='primary_sector',right_on='category_list')
