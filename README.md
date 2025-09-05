# covid_19_trendanalysis
basics of numpy ,pandas ,matplotlib
the code for covd trend_analysis:-

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.impute import SimpleImputer   
df = pd.read_csv(r'C:\Users\Vignesh\OneDrive\Desktop\abc devproject\covid_19_data.csv')
df.drop(['SNo','Last Update'],axis=1,inplace=True)
df.rename(columns={'ObservationDate':'Date','Province/State':'Provinance','Country/Region':'Country'},inplace=True)
df.head(10)
df['Date']=pd.to_datetime(df['Date'])
df['Date'] = pd.to_datetime(df['Date'])
imputer = SimpleImputer(strategy='constant')
df2 = pd.DataFrame(imputer.fit_transform(df), columns=df.columns)
df3 = df2.groupby(['Country','Date'])[['Confirmed', 'Deaths', 'Recovered']].sum().reset_index()
countries=df3['Country'].unique()
len(countries)
for idx in range(0,len(countries)):
    C=df3[df3['Country']==countries[idx]].reset_index()
    plt.scatter(np.arange(0,len(C)),C['Confirmed'],color='r',label='Confirmed')
    plt.scatter(np.arange(0,len(C)),C['Deaths'],color='g',label='Deaths')
    plt.scatter(np.arange(0,len(C)),C['Recovered'],color='b',label='Recovered')
    plt.title(countries[idx])
    plt.xlabel('Days since first suspect')
    plt.ylabel('Number of cases')
    plt.legend()
    # for world graph:
    df4 = df3.groupby(['Date'])[['Confirmed', 'Deaths', 'Recovered']].sum().reset_index()
    A=df4
    plt.scatter(np.arange(0,len(A)),A['Confirmed'],color='b',label='Confirmed')
plt.scatter(np.arange(0,len(A)),A['Deaths'],color='g',label='Deaths')
plt.scatter(np.arange(0,len(A)),A['Recovered'],color='r',label='Recovered')
plt.title('World')
plt.xlabel('Days since first suspect')
plt.ylabel('Number of cases')
plt.legend()
plt.show()
