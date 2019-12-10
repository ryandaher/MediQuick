import pandas as pd
import matplotlib.pyplot as plt
import PySimpleGUI as sg
from mpl_toolkits import mplot3d

#runs the program
def run():
    layout = [[sg.Text('Please Input Data')],
              [sg.Input(), sg.FileBrowse()],
              [sg.Submit(), sg.Cancel()]]

    window = sg.Window('MediQuick', layout)

    event, dfloc = window.Read()
    window.close()

    dflocs = str(dfloc)
    if dflocs[-5:-2] != 'csv':
        print('Please Upload a CSV')
        return

    df = pd.read_csv(dfloc[0], sep=',')
    chartselect(df)

#Selects the Chart
def chartselect(df):
    layout = [[sg.Text('Please Select Your Insight')],
              [sg.Radio('Demography', "RADIO1", default=True),sg.Radio('Demography Vs Price', "RADIO1")],
              [sg.Radio('Smokers', "RADIO1")],
              [sg.Submit(),sg.Cancel()]]
    window = sg.Window('Testcheckbox', layout)

    event, tester = window.Read()
    print(tester[0])
    output(tester[0],tester[1],tester[2],df)

#Saves Chart Input and Displays Insight
def output(demo,dprice,smokers,df):
    if demo == True:
        demographics(df)
    elif dprice == True:
        agebmi(df)
    elif smokers == True:
        smokeplot(df)

#Demographics Information
def demographics(df):

    plt.subplot(2, 1, 1)
    childpie(df)

    plt.subplot(2, 1, 2)
    genderpie(df)

    plt.show()

#Clinic Smokers and Average Medical Cost
def smokeplot(df):
    smoket = ['No', 'Yes']
    plt.bar(df['Smoking'], df['MedCost']/df.shape[0], align='center', color=("lightblue"))
    plt.xticks(range(0, 2), smoket)
    plt.title('Average Smoker Medical Costs')
    plt.show()

#Number of Children Breakdown
def childpie(df):
    kid1 = 0
    kid2 = 0
    kid3 = 0
    kid4 = 0
    kid5 = 0
    for i in range(1,df.shape[0]):
        if df['Children'][i] == 1:
            kid1 = kid1 + 1
        elif df['Children'][i] == 2:
            kid2 = kid2 + 1
        elif df['Children'][i] == 3:
            kid3 = kid3 + 1
        elif df['Children'][i] == 4:
            kid4 = kid4 + 1
        else:
            kid5 = kid5 + 1

    sizes = [kid1, kid2, kid3, kid4, kid5]
    labels = ["1 Child", '2 Children', '3 Children', '4 Children', '5 Children']
    colors = ['yellowgreen', 'gold', 'lightskyblue', 'lightcoral', 'purple']
    patches, texts = plt.pie(sizes, colors=colors, labels= labels,shadow=True, startangle=90)
    plt.axis('equal')
    plt.tight_layout()
    plt.title('# of Children Breakdown')

#Gender Breakdown
def genderpie(df):
    males = 0
    females = 0
    for i in range(0, df.shape[0]):
        if df['Gender'][i] == 1:
            males = males +1
        else:
            females = females + 1

    sizes = [males, females]
    labels = ['Male', 'Female']
    colors = ['blue', 'pink']
    patches, texts = plt.pie(sizes, colors=colors, labels=labels, shadow=True, startangle=90)
    plt.axis('equal')
    plt.tight_layout()
    plt.title('Gender Breakdown')

#Client Age, BMI and Cost
def agebmi(df):
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')

    ax.scatter(df['Age'], df['BMI'], df['MedCost'], c='r', marker='o')

    ax.set_xlabel('Age')
    ax.set_ylabel('BMI')
    ax.set_zlabel('Medical Cost')

    plt.title('Age and BMI Impact on Costs')

    plt.show()

run()
