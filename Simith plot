#import matplotlib.pylab as pl 
import smithplot
from smithplot import SmithAxes
import pandas as pd
import math
import sys

import numpy as np
from matplotlib import rcParams, pyplot as pp

rcParams.update({"legend.numpoints": 3})

sys.path.append("..")


path="/home/deola/MANI_CIRUIT.s2p.csv"

###########################################################################################################
def DataClean():

    dataTest =pd.read_excel("/home/deola/MANI_CIRUIT.s2p.xlsx")
    #print (dataTest)
    dataTest = dataTest.reset_index(drop=True)
    dataTest=dataTest.drop(dataTest.columns[[0, 1, 2]], axis=1)
    dataTest=dataTest.drop(dataTest.index[[0,1,2]])
    dataTest = dataTest.reset_index(drop=True)
    head=dataTest.values[0].tolist()
    dataTest=dataTest.drop(dataTest.index[[0]])
    d=[]
    for i in range(124):
    	if  i<61:
    		continue
    	else:
    		d.append(int(i))
    
    dataTest=dataTest.drop(dataTest.index[[d]])
    dataTest = dataTest.reset_index(drop=True)
    d#ataTest.columns=head
    #print(head)
    dataTest=dataTest.drop(dataTest.index[[0]])
    dataTest=pd.DataFrame(dataTest.values, columns = head)
    dataTest.to_csv("/home/deola/MANI_CIRUIT.s2p.csv")
    
##################################################################################################    
def ExecToCSV():
    dataTest =pd.read_excel("/home/deola/CE_CASCODE_KESI_DEGE_1.csv.xlsx")
    print (dataTest)
    #dataTest=pd.DataFrame(dataTest.values)
    #dataTest.to_csv("/home/deola/CE_CASCODE_KESI_DEGE_1.csv.csv")
#############################################################################################################
def GetArray(indexMag, indexAng):
    mag=list()
    ang=list()
    res=list()
    data=pd.read_csv("/home/deola/CE_CASCODE_KESI_1.csv")
    data=data.values
    mag=data[:,indexMag]
    ang=data[:,indexAng]
    print(mag)
    print("##########################################")
    print("##########################################")
    print (ang )
    
#############################################################################################################
def PolarToRectangluar(indexMag, indexAng, Angval=False):
    mag=list()
    ang=list()
    res=list()
    
    data=pd.read_csv(path)
    data=data.values
    mag=data[:,indexMag]
    ang=data[:,indexAng]
    #print(ang)
    
    for i in range(len(mag)):
        
        if Angval==False:
            #res.append((mag[i]*math.cos(ang[i])))
            res.append( mag[i]*math.cos(math.radians(ang[i])))
        else:
            res.append(mag[i]*math.sin(math.radians(ang[i])))
        #print (math.sin(math.radians(ang[i])))
    return (res)


    
############################################################################################################
def CreateCSV(name):
     
    
    val_S11Re=PolarToRectangluar(2,3)
    val_S11Im=PolarToRectangluar(2,3, True)
    val_S21Re=PolarToRectangluar(4,5)
    val_S21Im=PolarToRectangluar(4,5, True)
    val_S12Re=PolarToRectangluar(6,7)
    val_S12Im=PolarToRectangluar(6,7, True)
    val_S22Re=PolarToRectangluar(8,9)
    val_S22Im=PolarToRectangluar(8,9, True)
    
    val=pd.DataFrame(val_S11Re, columns=['val_S11Re'])
    val['val_S11Im']=val_S11Im
    val['val_S21Re']=val_S21Re
    val['val_S21Im']=val_S21Im
    val['val_S12Re']=val_S12Re
    val['val_S12Im']=val_S12Im
    val['val_S22Re']=val_S22Re
    val['val_S22Im']=val_S22Im
    
    val.to_csv("/home/deola/%s"%(name))
    print("CSV completed")
#########################################################################################################################    
def SmithPlotting(name):
    
    data=pd.read_csv("/home/deola/%s"%(name))
    data=data.values
    #val_S11=data[:,1]
    #val_S21=data[:,2]
    #val_S12=data[:,3]
    #val_S22=data[:,4]
    #val_S11 = ','.join(map(str, val_S11)) 
    
    data = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/main_circuit_12022018_D.s2p.csv", delimiter=",", skiprows=1)[::10]
    val1 = 0.02*data[:, 1] + 0.02*data[:, 2] * 1j

    data2 = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/main_circuit_12022018_ND.s2p33.csv", delimiter=",", skiprows=1)[::10]
    val2 = 0.02*data2[:, 1] + 0.02*data2[:, 2] * 1j
    #print (val2)

    
    #data = np.loadtxt("/home/deola/CE_CASCODE_KESI_DEGE_1.csv", delimiter=",", skiprows=1)[::10]
    #val3 = data[:, 7] + data[:, 6] * 1j

    #data = np.loadtxt("/home/deola/CE_CASCODE_KESI_DEGE_1.csv", delimiter=",", skiprows=1)[::10]
    #val4 = data[:, 7] + data[:, 8] * 1j

    
    # plot data
    pp.figure(figsize=(6, 6))

    ax = pp.subplot(1, 1, 1, projection='smith')
    #pp.plot([1, 10], markevery=1)
    pp.plot(val1, markevery=1,marker='+',color='magenta', markeredgecolor='blue',label="S11", equipoints=40, datatype=SmithAxes.S_PARAMETER)
    pp.plot(val2, markevery=1, color='red',label="S21", equipoints=60,marker='*', datatype=SmithAxes.S_PARAMETER)

    #pp.plot(val3, markevery=1, label="equipoints=22", equipoints=15, datatype=SmithAxes.S_PARAMETER)
    #pp.plot(val4, markevery=3, label="equipoints=22, \nmarkevery=3", equipoints=15, datatype=SmithAxes.S_PARAMETER)

    pp.legend(loc="upper left", fontsize=12)
    pp.title("Smith chart")
    
    pp.savefig("/home/deola/Documents/Paper_for_Bottle_classification/export.pdf", format="pdf", bbox_inches="tight")
    pp.savefig('/home/deola/Documents/Paper_for_Bottle_classification/smith.eps', format='eps', dpi=300)
    print("Finish plotting")
    
############################################################################################################################
def PlotNoise():
    
    data = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/testing_noise_plotting_D.s2p.csv", delimiter=",", skiprows=1)[::10]
    data1 = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/testing_noise_plotting_ND.s2p.csv", delimiter=",", skiprows=1)[::10]
    val1 = data[:, 0]
    val2= data[:, 1]
    val3 = data1[:, 0]
    val4 = data1[:, 1]
   
    #ax = pp.grid(color='r', linestyle='-', linewidth=2)   
    pp.plot(val1, val2, marker='H',label="Noise_S1")
    pp.plot(val3, val4, marker='*',label="Noise_S2")
    pp.legend(loc="upper left", fontsize=12)
    pp.xlabel('Frequency')
    pp.ylabel('dB')
    pp.title("Frequency versus noise")
    pp.savefig('/home/deola/Documents/Paper_for_Bottle_classification/smith1.eps', format='eps', dpi=300)
    print("Finish plotting")
    #pp.show()
#################################################################################################################
def PlotGain():
    
    data = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/gAIN_testing_noise_plotting_D1.s2p.csv", delimiter=",", skiprows=1)[::10]
    data1 = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/gAIN_testing_noise_plotting_ND1.s2p.csv", delimiter=",", skiprows=1)[::10]
    val1 = data[:, 0]
    val2= data[:, 1]
    val3 = data1[:, 0]
    val4 = data1[:, 1]
    #ax = pp.grid(color='r', linestyle='-', linewidth=2)   
    pp.plot(val1, val2, marker='h',label="Gain_S1")
    pp.plot(val3, val4, marker='*',label="Gain_S2",color='red')
    pp.legend(loc="upper left", fontsize=12)
    pp.xlabel('Frequency')
    pp.ylabel('dB')
    pp.title("Frequency versus gain")
    pp.savefig('/home/deola/Documents/Paper_for_Bottle_classification/smith2.eps', format='eps', dpi=300)
    print("Finish plotting")
    #pp.show() 
    
    
################################################################################################################
def PlotCombo():
    
    data = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/testing_noise_plotting_D.s2p.csv", delimiter=",", skiprows=1)[::1]
    data1 = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/testing_noise_plotting_ND.s2p.csv", delimiter=",", skiprows=1)[::1]
    val1 = data[:, 0]
    val2= data[:, 1]
    val3 = data1[:, 0]
    val4 = data1[:, 1]
    data2 = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/gAIN_testing_noise_plotting_D1.s2p.csv", delimiter=",", skiprows=1)[::1]
    data3 = np.loadtxt("/home/deola/Documents/Paper_for_Bottle_classification/Dr_Kcee/gAIN_testing_noise_plotting_ND1.s2p.csv", delimiter=",", skiprows=1)[::1]
    val5 = data2[:, 0]   
    val6= data2[:, 1]
    val7 = data3[:, 0]
    val8 = data3[:, 1]
    #ax = pp.grid(color='r', linestyle='-', linewidth=2)   
    pp.plot(val1, val2, marker='+',label="Noise_S1")
    pp.plot(val3, val4, marker='*',label="Noise_S2")
    pp.plot(val5, val6, marker='>',label="Gain_S1")
    pp.plot(val7, val8, marker='o',label="Gain_S2")
    pp.xlabel('Frequency GHz')
    pp.ylabel('dB')
    pp.legend(loc="upper left", fontsize=12)
    pp.title("Frequency versus noise and gain")
    pp.savefig('/home/deola/Documents/Paper_for_Bottle_classification/smith4.eps', format='eps', dpi=300)
    print("Finish plotting")    
    
def addarr(ar):
    for i in ar:
        i+=i
    print i
############################################################################################################
############################################################################################################
##########################################################################################################


if __name__=="__main__":
    
    #DataClean()
    #GetArray(2,3)
    #PolarToRectangluar(4,5)
    #CreateCSV("MANI_CIRUIT.Val.csv")
    #ExecToCSV()
    #SmithPlotting("MANI_CIRUIT.Val.csv")
    #PlotNoise()
    #PlotGain()
    #PlotCombo()
