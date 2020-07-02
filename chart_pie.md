#Plot 1
import matplotlib.pyplot as plt
# Pie chart
labels = 'Angel - 0.97M', 'Venture - 11.7M', 'Seed - 0.74M', 'Private Equity - 71.3M'
sizes = [0.47, 61, 1.7, 14.13]
 
figure1, axis1 = plt.subplots()
axis1.pie(sizes, labels=labels, autopct='%1.0f%%', startangle=90)
#draw circle
centre_circle = plt.Circle((0,0),0.70,fc='white')
figure1 = plt.gcf()
figure1.gca().add_artist(centre_circle)
# Equal aspect ratio ensures that pie is drawn as a circle
axis1.axis('equal')  
plt.tight_layout()
plt.show()