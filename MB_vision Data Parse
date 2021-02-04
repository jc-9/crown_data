

# !/usr/bin/env python3

"""

Justin Clay

FEB_02_2021

"""

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from datetime import date

# Input File Path of the CSV File and press go!
file = 'C:\\Users\melma\PycharmProjects\Plot\Data_logs\JUUL_2021-02-04T1116.csv'

col_list = [

    'BARCODE CHECK.Barcode_Measurment - BarcodeHeight',

    'BARCODE CHECK.Barcode_Measurment - BarcodeWidth',

    'BARCODE CHECK.Barcode_Measurment - BarcodePosY',

    'BARCODE CHECK.Barcode_Measurment - LowerCenterPoint_X',

    'BARCODE CHECK.Barcode_Measurment - UpperCenterPoint_X',

    'FINAL CHECK.Final_Module Tilt - HeightDifferenceBottom',

    'FINAL CHECK.Final_Module Tilt - HeightDifferenceTop',

    'POST EPOXY/PRE PLACE/POST PLACE.Post_Place_Check_Module Width and Height: GEOMEAS - LowerCenterPoint_X',

    'POST EPOXY/PRE PLACE/POST PLACE.Post_Place_Check_Module Width and Height: GEOMEAS - UpperCenterPoint_X',

    'POST EPOXY/PRE PLACE/POST PLACE.Post_Place_Check_Module Width and Height: GEOMEAS - Width'

]

collist2 = [

    "Barcode DIM 12 ",

    "Barcode DIM 14",

    'Barcode DIM 13',

    'Barcode DIM 15/1',

    'Barcode DIM 15/2',

    'Chip Tilt DIM 18',

    'Chip Tilt DIM 7',

    'Chip Position DIM 4/1',

    'Chip Position DIM 4/2',

    'Chip Width DIM 1']

df = pd.read_csv(file, sep=';', usecols=col_list)

df_glueArea = pd.read_csv(file, sep=';', usecols=[

    'POST EPOXY/PRE PLACE/POST PLACE.Post_Epoxy_Pre_Place_Check_Epoxy_Position&Size: OBJMEAS - TotalArea'])

df = df.rename(columns={

    col_list[0]: collist2[0],

    col_list[1]: collist2[1],

    col_list[2]: collist2[2],

    col_list[3]: collist2[3],

    col_list[4]: collist2[4],

    col_list[5]: collist2[5],

    col_list[6]: collist2[6],

    col_list[7]: collist2[7],

    col_list[8]: collist2[8],

    col_list[9]: collist2[9],

})

df3 = df.dropna()

df_glueArea.dropna(inplace=True)

today = date.today()

d1 = today.strftime("%m/%d/%Y")

colm = df.shape[1]

n = rows = df.shape[0]

# New Spec Limits

BC_DIM12_USL = 2.24 + .10

BC_DIM12_LSL = 2.24 - .10

BC_DIM14_USL = 2.24 + .10

BC_DIM14_LSL = 2.24 - .10

BC_DIM13_USL = .66 + .30

BC_DIM13_LSL = .66 - .30

BC_DIM15_1_USL = .30

BC_DIM15_1_LSL = -.30

BC_DIM15_2_USL = .30

BC_DIM15_2_LSL = -.30

CT_DIM18_LSL = .9

CT_DIM7_LSL = .9

CP_DIM4_1_USL = .15

CP_DIM4_1_LSL = -.15

CP_DIM4_2_USL = .15

CP_DIM4_2_LSL = -.15

CW_DIM1_USL = 3.2 + .08

CW_DIM1_LSL = 3.2 - .08


# Old Spec Limits Feb 02 2020

# BC_DIM12_USL = 2.24 + .10

# BC_DIM12_LSL = 2.24 - .10

# BC_DIM14_USL = 2.24 + .10

# BC_DIM14_LSL = 2.24 - .10

# BC_DIM13_USL = .66 + .15

# BC_DIM13_LSL = .66 - .15

# BC_DIM15_1_USL = .15

# BC_DIM15_1_LSL = -.15

# BC_DIM15_2_USL = .15

# BC_DIM15_2_LSL = -.15

# CT_DIM18_LSL = .9

# CT_DIM7_LSL = .9

# CP_DIM4_1_USL = .15

# CP_DIM4_1_LSL = -.15

# CP_DIM4_2_USL = .15

# CP_DIM4_2_LSL = -.15

# CW_DIM1_USL = 3.2 + .08

# CW_DIM1_LSL = 3.2 - .08


def cpk(df, USL, LSL):
    CPKU = (USL - df.mean()) / (3 * df.std())

    CPKL = (df.mean() - LSL) / (3 * df.std())

    CPK = round(min(CPKU, CPKL), 3)

    if CPK <= 1.33:

        a = ' FAIL'

    else:

        a = ' PASS'

    return CPK, CPKU, CPKL, a


fig = plt.figure(figsize=(11, 11))

fig2 = plt.figure(figsize=(11, 11))

# fig.suptitle(f'MB Vision Analysis, n={rows} \n {file.split("/")[3]}')

ax1 = fig.add_subplot(521)

ax2 = fig.add_subplot(522)

ax3 = fig.add_subplot(523)

ax4 = fig.add_subplot(524)

ax5 = fig.add_subplot(525)

ax6 = fig.add_subplot(526)

ax7 = fig.add_subplot(527)

ax8 = fig.add_subplot(528)

ax9 = fig.add_subplot(529)

ax10 = fig.add_subplot(5, 2, 10)

bx1 = fig2.add_subplot(111)

ax1.boxplot(df3[collist2[0]])

cpk_ax1, _, _, z = cpk(df3[collist2[0]], BC_DIM12_USL, BC_DIM12_LSL)

ax1Labels = ax1.get_xticks()

ax1Labels = [collist2[0] + f',CPK:{round(cpk_ax1, 3)}' + z]

ax1.set_xticklabels(ax1Labels, rotation=0, color='black')

ax1.axhline(BC_DIM12_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'BC_DIM12_USL {BC_DIM12_USL}')

ax1.axhline(BC_DIM12_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'BC_DIM12_LSL {BC_DIM12_LSL}')

ax2.boxplot(df3[collist2[1]])

ax2Labels = ax2.get_xticks()

cpk_ax2, _, _, z = cpk(df3[collist2[1]], BC_DIM14_USL, BC_DIM14_LSL)

ax2Labels = [collist2[1] + f',CPK:{round(cpk_ax2, 3)}' + z]

ax2.set_xticklabels(ax2Labels, rotation=0, color='black')

ax2.axhline(BC_DIM14_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'BC_DIM14_USL {BC_DIM14_USL}')

ax2.axhline(BC_DIM14_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'BC_DIM14_LSL {BC_DIM14_LSL}')

ax3.boxplot(df3[collist2[2]])

cpk_ax3, _, _, z = cpk(df3[collist2[2]], BC_DIM13_USL, BC_DIM13_LSL)

ax3Labels = ax3.get_xticks()

ax3Labels = [collist2[2] + f',CPK:{round(cpk_ax3, 3)}' + z]

ax3.set_xticklabels(ax3Labels, rotation=0, color='black')

ax3.axhline(BC_DIM13_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'BC_DIM13_USL {BC_DIM13_USL}')

ax3.axhline(BC_DIM13_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'BC_DIM13_LSL {BC_DIM13_LSL}')

ax4.boxplot(df3[collist2[3]])

cpk_ax4, _, _, z = cpk(df3[collist2[3]], BC_DIM15_1_USL, BC_DIM15_1_LSL)

ax4Labels = ax4.get_xticks()

ax4Labels = [collist2[3] + f',CPK:{round(cpk_ax4, 3)}' + z]

ax4.set_xticklabels(ax4Labels, rotation=0, color='black')

ax4.axhline(BC_DIM15_1_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'BC_DIM15_1_USL {BC_DIM15_1_USL}')

ax4.axhline(BC_DIM15_1_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'BC_DIM15_1_LSL {BC_DIM15_1_LSL}')

ax5.boxplot(df3[collist2[4]])

cpk_ax5, _, _, z = cpk(df3[collist2[4]], BC_DIM15_2_USL, BC_DIM15_2_LSL)

ax5Labels = ax5.get_xticks()

ax5Labels = [collist2[4] + f',CPK:{round(cpk_ax5, 3)}' + z]

ax5.set_xticklabels(ax5Labels, rotation=0, color='black')

ax5.axhline(BC_DIM15_2_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'BC_DIM15_2_USL {BC_DIM15_2_USL}')

ax5.axhline(BC_DIM15_2_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'BC_DIM15_2_LSL {BC_DIM15_2_LSL}')

ax6.boxplot(df3[collist2[5]])

_, _, cpl_ax6, z = cpk(df3[collist2[5]], _, CT_DIM18_LSL)

ax6Labels = ax6.get_xticks()

ax6Labels = [collist2[5] + f',CPK:{round(cpl_ax6, 3)}' + z]

ax6.set_xticklabels(ax6Labels, rotation=0, color='black')

ax6.axhline(CT_DIM18_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'CT_DIM18_LSL {CT_DIM18_LSL}')

ax7.boxplot(df3[collist2[6]])

_, _, cpl_ax7, z = cpk(df3[collist2[6]], _, CT_DIM7_LSL)

ax7Labels = ax7.get_xticks()

ax7Labels = [collist2[6] + f',CPK:{round(cpl_ax7, 3)}' + z]

ax7.set_xticklabels(ax7Labels, rotation=0, color='black')

ax7.axhline(CT_DIM7_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'CT_DIM7_LSL {CT_DIM7_LSL}')

ax8.boxplot(df3[collist2[7]])

cpk_ax8, _, _, z = cpk(df3[collist2[7]], CP_DIM4_1_USL, CP_DIM4_1_LSL)

ax8Labels = ax8.get_xticks()

ax8Labels = [collist2[7] + f',CPK:{round(cpk_ax8, 3)}' + z]

ax8.set_xticklabels(ax8Labels, rotation=0, color='black')

ax8.axhline(CP_DIM4_1_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'CP_DIM4_1_USL {CP_DIM4_1_USL}')

ax8.axhline(CP_DIM4_1_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'CP_DIM4_1_LSL {CP_DIM4_1_LSL}')

ax9.boxplot(df3[collist2[8]])

cpk_ax9, _, _, z = cpk(df3[collist2[8]], CP_DIM4_2_USL, CP_DIM4_2_LSL)

ax9Labels = ax8.get_xticks()

ax9Labels = [collist2[8] + f',CPK:{round(cpk_ax9, 3)}' + z]

ax9.set_xticklabels(ax9Labels, rotation=0, color='black')

ax9.axhline(CP_DIM4_2_USL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='r',

            label=f'CP_DIM4_2_USL {CP_DIM4_2_USL}')

ax9.axhline(CP_DIM4_2_LSL,

            xmin=0,

            xmax=1,

            linewidth=1,

            color='b',

            label=f'CP_DIM4_2_LSL {CP_DIM4_2_LSL}')

ax10.boxplot(df3[collist2[9]])

cpk_ax10, _, _, z = cpk(df3[collist2[9]], CW_DIM1_USL, CW_DIM1_LSL)

ax10Labels = ax10.get_xticks()

ax10Labels = [collist2[9] + f',CPK:{round(cpk_ax10, 3)}' + z]

ax10.set_xticklabels(ax10Labels, rotation=0, color='black')

ax10.axhline(CW_DIM1_USL,

             xmin=0,

             xmax=1,

             linewidth=1,

             color='r',

             label=f'CW_DIM1_USL {CW_DIM1_USL}')

ax10.axhline(CW_DIM1_LSL,

             xmin=0,

             xmax=1,

             linewidth=1,

             color='b',

             label=f'CW_DIM1_LSL {CW_DIM1_LSL}')

bx1.hist(df_glueArea, bins=50)

bx1.axvline(df_glueArea.mean()[0] + 3 * df_glueArea.std()[0], ymin=0, ymax=1, color='blue', label=f'+3 Sigma'

                                                                                                  f' {round(df_glueArea.mean()[0] + 3 * df_glueArea.std()[0], 2)}')

bx1.axvline(df_glueArea.mean()[0] - 3 * df_glueArea.std()[0], ymin=0, ymax=1, color='red', label=f'+3 Sigma'

                                                                                                 f' {round(df_glueArea.mean()[0] - 3 * df_glueArea.std()[0], 2)}')

plt.axvline(df_glueArea.mean()[0], ymin=0, ymax=1, color='green', label=f'Mean {round(df_glueArea.mean()[0], 2)}')

bx1.legend(loc='upper right')

bx1.set_title(f'Glue Area UV Highlight MB Algorithm \n 745-00040 \n {d1}, n={n}', color='black',

              fontsize=10)

plt.xlabel('mm^2')

plt.show()
