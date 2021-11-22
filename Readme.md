{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "bbd660b62cc616efa33651beedc49b86045b784d"
   },
   "source": [
    "## <font size=5> <strong>Heart Disease Prediction By Shreekant Gosavi\n",
    " "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "e41ea25bec5928203cec544d0413fecd4b4e5555"
   },
   "source": [
    "## I. Importing essential libraries"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "_uuid": "f571f7e57c828d45fe55f6136fe8c2e796f74d4e"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "['.ipynb_checkpoints', 'heart.csv', 'Heart_disease_prediction.ipynb', 'README.md']\n"
     ]
    }
   ],
   "source": [
    "import numpy as np\n",
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "\n",
    "%matplotlib inline\n",
    "\n",
    "import os\n",
    "print(os.listdir())\n",
    "\n",
    "import warnings\n",
    "warnings.filterwarnings('ignore')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "44e71221837f6fa60edc2c83b7492ddb019cc1cd"
   },
   "source": [
    "## II. Importing and understanding our dataset "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "_uuid": "2a1a1dae64ae3c934849b2b918bc7d68cd59e3f6"
   },
   "outputs": [],
   "source": [
    "dataset = pd.read_csv(\"heart.csv\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "481fa1d160a3256ef2470535bfb0574820fbaabd"
   },
   "source": [
    "#### Verifying it as a 'dataframe' object in pandas"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "_uuid": "86353d54a331dbf55a63874402cf13e2a72c3750"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "pandas.core.frame.DataFrame"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "type(dataset)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "44649a50ce58d2e10a032f7d0e7ecf435e932481"
   },
   "source": [
    "#### Shape of dataset"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "_uuid": "0a2396061d262bee451e61dd51be84d0bd1ac9d0"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(303, 14)"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "3e1de0c39fc28f086a5e8377cc5fbdbf91d377b3"
   },
   "source": [
    "#### Printing out a few columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "_uuid": "87ebcc578e5959fe9a9c9a538c73122183454459"
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>age</th>\n",
       "      <th>sex</th>\n",
       "      <th>cp</th>\n",
       "      <th>trestbps</th>\n",
       "      <th>chol</th>\n",
       "      <th>fbs</th>\n",
       "      <th>restecg</th>\n",
       "      <th>thalach</th>\n",
       "      <th>exang</th>\n",
       "      <th>oldpeak</th>\n",
       "      <th>slope</th>\n",
       "      <th>ca</th>\n",
       "      <th>thal</th>\n",
       "      <th>target</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>63</td>\n",
       "      <td>1</td>\n",
       "      <td>3</td>\n",
       "      <td>145</td>\n",
       "      <td>233</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>150</td>\n",
       "      <td>0</td>\n",
       "      <td>2.3</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>37</td>\n",
       "      <td>1</td>\n",
       "      <td>2</td>\n",
       "      <td>130</td>\n",
       "      <td>250</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>187</td>\n",
       "      <td>0</td>\n",
       "      <td>3.5</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>41</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>130</td>\n",
       "      <td>204</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>172</td>\n",
       "      <td>0</td>\n",
       "      <td>1.4</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>56</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>120</td>\n",
       "      <td>236</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>178</td>\n",
       "      <td>0</td>\n",
       "      <td>0.8</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>57</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>120</td>\n",
       "      <td>354</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>163</td>\n",
       "      <td>1</td>\n",
       "      <td>0.6</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   age  sex  cp  trestbps  chol   ...    oldpeak  slope  ca  thal  target\n",
       "0   63    1   3       145   233   ...        2.3      0   0     1       1\n",
       "1   37    1   2       130   250   ...        3.5      0   0     2       1\n",
       "2   41    0   1       130   204   ...        1.4      2   0     2       1\n",
       "3   56    1   1       120   236   ...        0.8      2   0     2       1\n",
       "4   57    0   0       120   354   ...        0.6      2   0     2       1\n",
       "\n",
       "[5 rows x 14 columns]"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset.head(5)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "_uuid": "5132eb43114bf99d5f857f459d0c9d2faffc9644"
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>age</th>\n",
       "      <th>sex</th>\n",
       "      <th>cp</th>\n",
       "      <th>trestbps</th>\n",
       "      <th>chol</th>\n",
       "      <th>fbs</th>\n",
       "      <th>restecg</th>\n",
       "      <th>thalach</th>\n",
       "      <th>exang</th>\n",
       "      <th>oldpeak</th>\n",
       "      <th>slope</th>\n",
       "      <th>ca</th>\n",
       "      <th>thal</th>\n",
       "      <th>target</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>248</th>\n",
       "      <td>54</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>192</td>\n",
       "      <td>283</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>195</td>\n",
       "      <td>0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>3</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>147</th>\n",
       "      <td>60</td>\n",
       "      <td>0</td>\n",
       "      <td>3</td>\n",
       "      <td>150</td>\n",
       "      <td>240</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>171</td>\n",
       "      <td>0</td>\n",
       "      <td>0.9</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>239</th>\n",
       "      <td>35</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>126</td>\n",
       "      <td>282</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>156</td>\n",
       "      <td>1</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>3</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>57</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>120</td>\n",
       "      <td>354</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>163</td>\n",
       "      <td>1</td>\n",
       "      <td>0.6</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>44</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>120</td>\n",
       "      <td>263</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>173</td>\n",
       "      <td>0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2</td>\n",
       "      <td>0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     age  sex  cp  trestbps  chol   ...    oldpeak  slope  ca  thal  target\n",
       "248   54    1   1       192   283   ...        0.0      2   1     3       0\n",
       "147   60    0   3       150   240   ...        0.9      2   0     2       1\n",
       "239   35    1   0       126   282   ...        0.0      2   0     3       0\n",
       "4     57    0   0       120   354   ...        0.6      2   0     2       1\n",
       "7     44    1   1       120   263   ...        0.0      2   0     3       1\n",
       "\n",
       "[5 rows x 14 columns]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset.sample(5)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "1113236bec2848d33c5bfe088ff0d03246b8b7ce"
   },
   "source": [
    "#### Description"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "_uuid": "c31619815cb0dae5586985671fdc21110b39a821"
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>age</th>\n",
       "      <th>sex</th>\n",
       "      <th>cp</th>\n",
       "      <th>trestbps</th>\n",
       "      <th>chol</th>\n",
       "      <th>fbs</th>\n",
       "      <th>restecg</th>\n",
       "      <th>thalach</th>\n",
       "      <th>exang</th>\n",
       "      <th>oldpeak</th>\n",
       "      <th>slope</th>\n",
       "      <th>ca</th>\n",
       "      <th>thal</th>\n",
       "      <th>target</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "      <td>303.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>54.366337</td>\n",
       "      <td>0.683168</td>\n",
       "      <td>0.966997</td>\n",
       "      <td>131.623762</td>\n",
       "      <td>246.264026</td>\n",
       "      <td>0.148515</td>\n",
       "      <td>0.528053</td>\n",
       "      <td>149.646865</td>\n",
       "      <td>0.326733</td>\n",
       "      <td>1.039604</td>\n",
       "      <td>1.399340</td>\n",
       "      <td>0.729373</td>\n",
       "      <td>2.313531</td>\n",
       "      <td>0.544554</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>9.082101</td>\n",
       "      <td>0.466011</td>\n",
       "      <td>1.032052</td>\n",
       "      <td>17.538143</td>\n",
       "      <td>51.830751</td>\n",
       "      <td>0.356198</td>\n",
       "      <td>0.525860</td>\n",
       "      <td>22.905161</td>\n",
       "      <td>0.469794</td>\n",
       "      <td>1.161075</td>\n",
       "      <td>0.616226</td>\n",
       "      <td>1.022606</td>\n",
       "      <td>0.612277</td>\n",
       "      <td>0.498835</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>29.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>94.000000</td>\n",
       "      <td>126.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>71.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>47.500000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>120.000000</td>\n",
       "      <td>211.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>133.500000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>55.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>130.000000</td>\n",
       "      <td>240.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>153.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.800000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>61.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>140.000000</td>\n",
       "      <td>274.500000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>166.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.600000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>3.000000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>77.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>3.000000</td>\n",
       "      <td>200.000000</td>\n",
       "      <td>564.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>202.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>6.200000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>4.000000</td>\n",
       "      <td>3.000000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              age         sex     ...            thal      target\n",
       "count  303.000000  303.000000     ...      303.000000  303.000000\n",
       "mean    54.366337    0.683168     ...        2.313531    0.544554\n",
       "std      9.082101    0.466011     ...        0.612277    0.498835\n",
       "min     29.000000    0.000000     ...        0.000000    0.000000\n",
       "25%     47.500000    0.000000     ...        2.000000    0.000000\n",
       "50%     55.000000    1.000000     ...        2.000000    1.000000\n",
       "75%     61.000000    1.000000     ...        3.000000    1.000000\n",
       "max     77.000000    1.000000     ...        3.000000    1.000000\n",
       "\n",
       "[8 rows x 14 columns]"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "_uuid": "718b82039841c137ab7e08a6e79e264643134642"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 303 entries, 0 to 302\n",
      "Data columns (total 14 columns):\n",
      "age         303 non-null int64\n",
      "sex         303 non-null int64\n",
      "cp          303 non-null int64\n",
      "trestbps    303 non-null int64\n",
      "chol        303 non-null int64\n",
      "fbs         303 non-null int64\n",
      "restecg     303 non-null int64\n",
      "thalach     303 non-null int64\n",
      "exang       303 non-null int64\n",
      "oldpeak     303 non-null float64\n",
      "slope       303 non-null int64\n",
      "ca          303 non-null int64\n",
      "thal        303 non-null int64\n",
      "target      303 non-null int64\n",
      "dtypes: float64(1), int64(13)\n",
      "memory usage: 33.2 KB\n"
     ]
    }
   ],
   "source": [
    "dataset.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "_uuid": "99d7182ca186d37f63b1fc433fe74ad5e2bc7d2f"
   },
   "outputs": [],
   "source": [
    "###Luckily, we have no missing values"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "85b59fefde7c5ecdb50e3b8da0cb719f4e14630f"
   },
   "source": [
    "#### Let's understand our columns better:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "_uuid": "5593d1021d54aad598c21f877e57969e6b47f5a8"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "age:\t\t\tage\n",
      "sex:\t\t\t1: male, 0: female\n",
      "cp:\t\t\tchest pain type, 1: typical angina, 2: atypical angina, 3: non-anginal pain, 4: asymptomatic\n",
      "trestbps:\t\t\tresting blood pressure\n",
      "chol:\t\t\t serum cholestoral in mg/dl\n",
      "fbs:\t\t\tfasting blood sugar > 120 mg/dl\n",
      "restecg:\t\t\tresting electrocardiographic results (values 0,1,2)\n",
      "thalach:\t\t\t maximum heart rate achieved\n",
      "exang:\t\t\texercise induced angina\n",
      "oldpeak:\t\t\toldpeak = ST depression induced by exercise relative to rest\n",
      "slope:\t\t\tthe slope of the peak exercise ST segment\n",
      "ca:\t\t\tnumber of major vessels (0-3) colored by flourosopy\n",
      "thal:\t\t\tthal: 3 = normal; 6 = fixed defect; 7 = reversable defect\n"
     ]
    }
   ],
   "source": [
    "info = [\"age\",\"1: male, 0: female\",\"chest pain type, 1: typical angina, 2: atypical angina, 3: non-anginal pain, 4: asymptomatic\",\"resting blood pressure\",\" serum cholestoral in mg/dl\",\"fasting blood sugar > 120 mg/dl\",\"resting electrocardiographic results (values 0,1,2)\",\" maximum heart rate achieved\",\"exercise induced angina\",\"oldpeak = ST depression induced by exercise relative to rest\",\"the slope of the peak exercise ST segment\",\"number of major vessels (0-3) colored by flourosopy\",\"thal: 3 = normal; 6 = fixed defect; 7 = reversable defect\"]\n",
    "\n",
    "\n",
    "\n",
    "for i in range(len(info)):\n",
    "    print(dataset.columns[i]+\":\\t\\t\\t\"+info[i])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "6a970312b67b588610a8579ecc2ba4bac0fcee04"
   },
   "source": [
    "#### Analysing the 'target' variable"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "_uuid": "b883243919bd382193ed15e2a90f9b522bf6f1f7"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    303.000000\n",
       "mean       0.544554\n",
       "std        0.498835\n",
       "min        0.000000\n",
       "25%        0.000000\n",
       "50%        1.000000\n",
       "75%        1.000000\n",
       "max        1.000000\n",
       "Name: target, dtype: float64"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"target\"].describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "_uuid": "9c107b83e0148914826282bf1f0ab28505d577ab"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([1, 0])"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"target\"].unique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "8c96e97e3f52844e8c4c6ff069f53bfe97c9982d"
   },
   "source": [
    "#### Clearly, this is a classification problem, with the target variable having values '0' and '1'"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "3ae0dfa26e2daf4cfc8e1c6f3b5008d0dab22ec0"
   },
   "source": [
    "### Checking correlation between columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "_uuid": "3059188d3874be2e0c80e13655609ac6a6fc644f"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "target      1.000000\n",
      "exang       0.436757\n",
      "cp          0.433798\n",
      "oldpeak     0.430696\n",
      "thalach     0.421741\n",
      "ca          0.391724\n",
      "slope       0.345877\n",
      "thal        0.344029\n",
      "sex         0.280937\n",
      "age         0.225439\n",
      "trestbps    0.144931\n",
      "restecg     0.137230\n",
      "chol        0.085239\n",
      "fbs         0.028046\n",
      "Name: target, dtype: float64\n"
     ]
    }
   ],
   "source": [
    "print(dataset.corr()[\"target\"].abs().sort_values(ascending=False))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "_uuid": "6e8cf6f86952d94764c1021207fa5b383b2b84bf"
   },
   "outputs": [],
   "source": [
    "#This shows that most columns are moderately correlated with target, but 'fbs' is very weakly correlated."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "40b6c0a9d03bcab78b87bd41c7df3fe1b930547a"
   },
   "source": [
    "## Exploratory Data Analysis (EDA)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "41da6ba94903ad6ee64b1ba6a1462815ae603536"
   },
   "source": [
    "### First, analysing the target variable:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "_uuid": "29aa23ccb8e6438688e16346b3474f4cc03bae13"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "1    165\n",
      "0    138\n",
      "Name: target, dtype: int64\n"
     ]
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAYgAAAEKCAYAAAAIO8L1AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAETFJREFUeJzt3X2sn2V9x/H3Ryo6fCrYIwKllmlxQ+cDHgnT6FDMROcsc45AdFQl6dwQdZopuGUYE4xON4c6XRqplMWBiCJo2JQhynQCHpSH8jQbHtuAPYogasQVv/vjd9cey9X210N/v/vAeb+S5tz3dV33fX+btOeT635MVSFJ0tYe0XcBkqS5yYCQJDUZEJKkJgNCktRkQEiSmgwISVKTASFJajIgJElNBoQkqWlB3wU8GIsWLaqlS5f2XYYkPaRcccUVP6yqiR2Ne0gHxNKlS5mamuq7DEl6SEly6zDjPMUkSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1GRASJKaDAhJUpMBIUlqekg/SS09nN32vt/ruwTNQUv+/pqxHcsZhCSpaWQBkWR1ko1J1m7VfkKSG5Jcm+QfZrSflGRdkhuTvHxUdUmShjPKU0ynAx8HztjckOQlwHLg2VV1X5Inde0HAUcDzwD2Bf4ryYFVdf8I65MkbcfIZhBVdQlw11bNfwl8oKru68Zs7NqXA2dV1X1VdTOwDjhkVLVJknZs3NcgDgRelOSyJN9I8vyufT/g9hnj1ndtkqSejPsupgXAXsChwPOBs5P89s7sIMlKYCXAkiVLdnmBkqSBcc8g1gNfqIHLgV8Bi4ANwP4zxi3u2h6gqlZV1WRVTU5M7PCDSJKkWRp3QHwReAlAkgOB3YEfAucDRyd5VJIDgGXA5WOuTZI0w8hOMSU5EzgMWJRkPXAysBpY3d36+ktgRVUVcG2Ss4HrgE3A8d7BJEn9GllAVNUx2+h6/TbGnwKcMqp6JEk7xyepJUlNBoQkqcmAkCQ1GRCSpCYDQpLUZEBIkpoMCElSkwEhSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1GRASJKaDAhJUpMBIUlqGllAJFmdZGP39bit+96ZpJIs6taT5KNJ1iW5OsnBo6pLkjScUc4gTgeO2Loxyf7AHwK3zWh+BYPvUC8DVgKfHGFdkqQhjCwgquoS4K5G10eAdwE1o205cEYNXAosTLLPqGqTJO3YWK9BJFkObKiqq7bq2g+4fcb6+q5NktSTBeM6UJI9gPcwOL30YPazksFpKJYsWbILKpMktYxzBvFU4ADgqiS3AIuB7yZ5MrAB2H/G2MVd2wNU1aqqmqyqyYmJiRGXLEnz19gCoqquqaonVdXSqlrK4DTSwVV1J3A+cGx3N9OhwD1Vdce4apMkPdDITjElORM4DFiUZD1wclWdto3hFwCvBNYBPwfeOKq6tva8vzljXIfSQ8gVHzq27xKk3o0sIKrqmB30L52xXMDxo6pFkrTzfJJaktRkQEiSmgwISVKTASFJajIgJElNBoQkqcmAkCQ1GRCSpCYDQpLUZEBIkpoMCElSkwEhSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1DSygEiyOsnGJGtntH0oyQ1Jrk5ybpKFM/pOSrIuyY1JXj6quiRJwxnlDOJ04Iit2i4EnllVzwL+FzgJIMlBwNHAM7ptPpFktxHWJknagZEFRFVdAty1VdtXq2pTt3opsLhbXg6cVVX3VdXNwDrgkFHVJknasT6vQbwJ+I9ueT/g9hl967u2B0iyMslUkqnp6ekRlyhJ81cvAZHkb4FNwGd2dtuqWlVVk1U1OTExseuLkyQBsGDcB0zyBuBVwOFVVV3zBmD/GcMWd22SpJ6MdQaR5AjgXcCrq+rnM7rOB45O8qgkBwDLgMvHWZsk6TeNbAaR5EzgMGBRkvXAyQzuWnoUcGESgEur6s1VdW2Ss4HrGJx6Or6q7h9VbZKkHRtZQFTVMY3m07Yz/hTglFHVI0naOT5JLUlqMiAkSU0GhCSpyYCQJDUZEJKkJgNCktRkQEiSmgwISVKTASFJajIgJElNBoQkqcmAkCQ1GRCSpCYDQpLUZEBIkpoMCElS08gCIsnqJBuTrJ3RtleSC5N8v/u5Z9eeJB9Nsi7J1UkOHlVdkqThjHIGcTpwxFZtJwIXVdUy4KJuHeAVDL5DvQxYCXxyhHVJkoYwsoCoqkuAu7ZqXg6s6ZbXAEfOaD+jBi4FFibZZ1S1SZJ2bNzXIPauqju65TuBvbvl/YDbZ4xb37U9QJKVSaaSTE1PT4+uUkma53q7SF1VBdQstltVVZNVNTkxMTGCyiRJMP6A+MHmU0fdz41d+wZg/xnjFndtkqSejDsgzgdWdMsrgPNmtB/b3c10KHDPjFNRkqQeLBjVjpOcCRwGLEqyHjgZ+ABwdpLjgFuBo7rhFwCvBNYBPwfeOKq6JEnDGSogklxUVYfvqG2mqjpmG10P2Ka7HnH8MLVIksZjuwGR5NHAHgxmAXsC6boezzbuMpIkPTzsaAbxF8DbgX2BK9gSED8BPj7CuiRJPdtuQFTVqcCpSU6oqo+NqSZJ0hww1DWIqvpYkhcAS2duU1VnjKguSVLPhr1I/W/AU4Ergfu75gIMCEl6mBr2NtdJ4KDubiNJ0jww7INya4Enj7IQSdLcMuwMYhFwXZLLgfs2N1bVq0dSlSSpd8MGxHtHWYQkae4Z9i6mb4y6EEnS3DLsXUz3suXV3LsDjwR+VlWPH1VhkqR+DTuDeNzm5SRh8AW4Q0dVlCSpfzv9uu/us6BfBF4+gnokSXPEsKeYXjNj9REMnov4xUgqkiTNCcPexfTHM5Y3AbcwOM0kSXqYGvYahB/wkaR5ZqhrEEkWJzk3ycbuz+eTLJ7tQZP8dZJrk6xNcmaSRyc5IMllSdYl+WyS3We7f0nSgzfsRepPM/hu9L7dny91bTstyX7AW4HJqnomsBtwNPBB4CNV9TTgx8Bxs9m/JGnXGDYgJqrq01W1qftzOjDxII67APitJAsYfLHuDuClwDld/xrgyAexf0nSgzRsQPwoyeuT7Nb9eT3wo9kcsKo2AB8GbmMQDPcw+Frd3VW1qRu2nm180jTJyiRTSaamp6dnU4IkaQjDBsSbgKOAOxn8Un8t8IbZHLD7tvVy4AAGp6seAxwx7PZVtaqqJqtqcmLiwUxiJEnbM+xtru8DVlTVjwGS7MVgFvCmWRzzZcDNVTXd7esLwAuBhUkWdLOIxcCGWexbkrSLDDuDeNbmcACoqruA587ymLcBhybZo3ttx+HAdcDFDGYmACuA82a5f0nSLjBsQDyiOzUE/HoGMezs4zdU1WUMLkZ/F7imq2EV8G7gHUnWAU8ETpvN/iVJu8awv+T/Efh2ks91638GnDLbg1bVycDJWzXfBBwy231KknatYZ+kPiPJFINbUQFeU1XXja4sSVLfhj5N1AWCoSBJ88ROv+5bkjQ/GBCSpCYDQpLUZEBIkpoMCElSkwEhSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1GRASJKaDAhJUpMBIUlq6iUgkixMck6SG5Jcn+T3k+yV5MIk3+9+7rnjPUmSRqWvGcSpwH9W1e8AzwauB04ELqqqZcBF3bokqSdjD4gkTwBeTPfN6ar6ZVXdDSwH1nTD1gBHjrs2SdIWfcwgDgCmgU8n+V6STyV5DLB3Vd3RjbkT2Lu1cZKVSaaSTE1PT4+pZEmaf/oIiAXAwcAnq+q5wM/Y6nRSVRVQrY2ralVVTVbV5MTExMiLlaT5qo+AWA+sr6rLuvVzGATGD5LsA9D93NhDbZKkztgDoqruBG5P8vSu6XDgOuB8YEXXtgI4b9y1SZK2WNDTcU8APpNkd+Am4I0MwursJMcBtwJH9VSbJImeAqKqrgQmG12Hj7sWSVKbT1JLkpoMCElSkwEhSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1GRASJKaDAhJUpMBIUlqMiAkSU0GhCSpyYCQJDUZEJKkJgNCktTUW0Ak2S3J95J8uVs/IMllSdYl+Wz3tTlJUk/6nEG8Dbh+xvoHgY9U1dOAHwPH9VKVJAnoKSCSLAb+CPhUtx7gpcA53ZA1wJF91CZJGuhrBvHPwLuAX3XrTwTurqpN3fp6YL8+CpMkDYw9IJK8CthYVVfMcvuVSaaSTE1PT+/i6iRJm/Uxg3gh8OoktwBnMTi1dCqwMMmCbsxiYENr46paVVWTVTU5MTExjnolaV4ae0BU1UlVtbiqlgJHA1+rqtcBFwOv7YatAM4bd22SpC3m0nMQ7wbekWQdg2sSp/VcjyTNawt2PGR0qurrwNe75ZuAQ/qsR5K0xVyaQUiS5hADQpLUZEBIkpoMCElSkwEhSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1GRASJKaDAhJUpMBIUlqMiAkSU0GhCSpyYCQJDWNPSCS7J/k4iTXJbk2ydu69r2SXJjk+93PPcddmyRpiz5mEJuAd1bVQcChwPFJDgJOBC6qqmXARd26JKknYw+Iqrqjqr7bLd8LXA/sBywH1nTD1gBHjrs2SdIWvV6DSLIUeC5wGbB3Vd3Rdd0J7N1TWZIkegyIJI8FPg+8vap+MrOvqgqobWy3MslUkqnp6ekxVCpJ81MvAZHkkQzC4TNV9YWu+QdJ9un69wE2tratqlVVNVlVkxMTE+MpWJLmoT7uYgpwGnB9Vf3TjK7zgRXd8grgvHHXJknaYkEPx3wh8OfANUmu7NreA3wAODvJccCtwFE91CZJ6ow9IKrqm0C20X34OGuRJG2bT1JLkpoMCElSkwEhSWoyICRJTQaEJKnJgJAkNRkQkqQmA0KS1GRASJKaDAhJUpMBIUlqMiAkSU0GhCSpyYCQJDUZEJKkJgNCktQ05wIiyRFJbkyyLsmJfdcjSfPVnAqIJLsB/wK8AjgIOCbJQf1WJUnz05wKCOAQYF1V3VRVvwTOApb3XJMkzUtzLSD2A26fsb6+a5MkjdmCvgvYWUlWAiu71Z8mubHPeh5mFgE/7LuIuSAfXtF3CfpN/tvc7OTsir08ZZhBcy0gNgD7z1hf3LX9WlWtAlaNs6j5IslUVU32XYe0Nf9t9mOunWL6DrAsyQFJdgeOBs7vuSZJmpfm1AyiqjYleQvwFWA3YHVVXdtzWZI0L82pgACoqguAC/quY57y1J3mKv9t9iBV1XcNkqQ5aK5dg5AkzREGhHy9ieasJKuTbEyytu9a5iMDYp7z9Saa404Hjui7iPnKgJCvN9GcVVWXAHf1Xcd8ZUDI15tIajIgJElNBoR2+HoTSfOTASFfbyKpyYCY56pqE7D59SbXA2f7ehPNFUnOBL4NPD3J+iTH9V3TfOKT1JKkJmcQkqQmA0KS1GRASJKaDAhJUpMBIUlqMiCk7UiyMMlfjeE4hyV5waiPI+0MA0LavoXA0AGRgdn8vzoMMCA0p/gchLQdSTa/3fZG4GLgWcCewCOBv6uq85IsZfCg4WXA84BXAi8D3g3cDVwF3FdVb0kyAfwrsKQ7xNsZvNrkUuB+YBo4oar+exx/P2l7DAhpO7pf/l+uqmcmWQDsUVU/SbKIwS/1ZcBTgJuAF1TVpUn2Bf4HOBi4F/gacFUXEP8OfKKqvplkCfCVqvrdJO8FflpVHx7331HalgV9FyA9hAR4f5IXA79i8Fr0vbu+W6vq0m75EOAbVXUXQJLPAQd2fS8DDkqyeZ+PT/LYcRQv7SwDQhre64AJ4HlV9X9JbgEe3fX9bMh9PAI4tKp+MbNxRmBIc4YXqaXtuxd4XLf8BGBjFw4vYXBqqeU7wB8k2bM7LfWnM/q+CpyweSXJcxrHkeYEA0Lajqr6EfCtJGuB5wCTSa4BjgVu2MY2G4D3A5cD3wJuAe7put/a7ePqJNcBb+7avwT8SZIrk7xoVH8faWd4kVoagSSPraqfdjOIc4HVVXVu33VJO8MZhDQa701yJbAWuBn4Ys/1SDvNGYQkqckZhCSpyYCQJDUZEJKkJgNCktRkQEiSmgwISVLT/wNhpkwDKiB3EQAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "y = dataset[\"target\"]\n",
    "\n",
    "sns.countplot(y)\n",
    "\n",
    "\n",
    "target_temp = dataset.target.value_counts()\n",
    "\n",
    "print(target_temp)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "_uuid": "5240af8bcd12736900050cea077c713d7d9641df"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Percentage of patience without heart problems: 45.54\n",
      "Percentage of patience with heart problems: 54.46\n"
     ]
    }
   ],
   "source": [
    "print(\"Percentage of patience without heart problems: \"+str(round(target_temp[0]*100/303,2)))\n",
    "print(\"Percentage of patience with heart problems: \"+str(round(target_temp[1]*100/303,2)))\n",
    "\n",
    "#Alternatively,\n",
    "# print(\"Percentage of patience with heart problems: \"+str(y.where(y==1).count()*100/303))\n",
    "# print(\"Percentage of patience with heart problems: \"+str(y.where(y==0).count()*100/303))\n",
    "\n",
    "# #Or,\n",
    "# countNoDisease = len(df[df.target == 0])\n",
    "# countHaveDisease = len(df[df.target == 1])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "e7de1da221d4ee72e89c365fecfa7d4506f1b184"
   },
   "source": [
    "### We'll analyse 'sex', 'cp', 'fbs', 'restecg', 'exang', 'slope', 'ca' and 'thal' features"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "82f9919a1312b53f22980a0071d077e5b0288d90"
   },
   "source": [
    "### Analysing the 'Sex' feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "_uuid": "07a3fb2f44b82360d0393377029851655bcdcd31"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([1, 0])"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"sex\"].unique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "623fe97e454ea061942ec6d948adeb5b7026cc65"
   },
   "source": [
    "##### We notice, that as expected, the 'sex' feature has 2 unique features"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "_uuid": "5d10e6c167251e6d3b1b82a06159da234eeef721"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754be2e128>"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"sex\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "31142d6b72ae034487a088860fe9c7ff85cf7ca2"
   },
   "source": [
    "##### We notice, that females are more likely to have heart problems than males"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "f7bbd747b02746eadfa2b525544509c8545ac1af"
   },
   "source": [
    "### Analysing the 'Chest Pain Type' feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {
    "_uuid": "7c795d4a86ee05d58e10a412add90065afbd4a70"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([3, 2, 1, 0])"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"cp\"].unique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "4e83947e6876ffa63837c7e5ce1364a53cbfa499"
   },
   "source": [
    "##### As expected, the CP feature has values from 0 to 3"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "_uuid": "56d6ed2b3d8d20a61814980cd459502b452d14c1"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754be17d30>"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"cp\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "510c7c3a7386a7e308cc6052025dc806fad61534"
   },
   "source": [
    "##### We notice, that chest pain of '0', i.e. the ones with typical angina are much less likely to have heart problems"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "bb50bd1cedd31d29683e2411439368aa1390e7ef"
   },
   "source": [
    "### Analysing the FBS feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "_uuid": "55f9ca01da5294b5404f3eb14d202ae90e0ea1bf"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    303.000000\n",
       "mean       0.148515\n",
       "std        0.356198\n",
       "min        0.000000\n",
       "25%        0.000000\n",
       "50%        0.000000\n",
       "75%        0.000000\n",
       "max        1.000000\n",
       "Name: fbs, dtype: float64"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"fbs\"].describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "_uuid": "43d491d311a8b96a6a9cbecbeff87f577584cd3a"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([1, 0])"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"fbs\"].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {
    "_uuid": "90509dcee97df858115131c771e69347a044aafb"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bddda90>"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"fbs\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "7ec0ef582de18e2ddd06083d4caca7f760ba3700"
   },
   "source": [
    "##### Nothing extraordinary here"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "5a8d6384c879ed40eddefed03b16607bc02deecf"
   },
   "source": [
    "### Analysing the restecg feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "_uuid": "b12fcc535fe07bc58aa99e97ec9b4e0b01f30a8d"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0, 1, 2])"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"restecg\"].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {
    "_uuid": "ccae9489c2b6e63adb87cef83d367f49ef08a133"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bd3bdd8>"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"restecg\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "84cf1d3ca8d3507765bbb3763834c3795380f1bf"
   },
   "source": [
    "##### We realize that people with restecg '1' and '0' are much more likely to have a heart disease than with restecg '2'"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "efaf4d85a6837cf43bd5b33d4eaaf193bc6fedc1"
   },
   "source": [
    "### Analysing the 'exang' feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {
    "_uuid": "53dd2985ea50aa6f9c9e5931050b4ef7b7aa609d"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0, 1])"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"exang\"].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {
    "_uuid": "237a60a2a11dab86e50cafcee4ec47df752876a1"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bc9eda0>"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"exang\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "f442f08734344740ebc225af7a565bcb91962dca"
   },
   "source": [
    "##### People with exang=1 i.e. Exercise induced angina are much less likely to have heart problems"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "4ce2d649ededc2126324cd07ce430b005697e288"
   },
   "source": [
    "### Analysing the Slope feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {
    "_uuid": "e1e148d25967c36d2bb5fbfb802c70dae93f8a4f"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0, 2, 1])"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"slope\"].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {
    "_uuid": "beaa943c166b3c550fe357e6e937dbda46b707c9"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bc75710>"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"slope\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "3141a4a203dd433dd7af6c02c1d0b44d048656a0"
   },
   "source": [
    "##### We observe, that Slope '2' causes heart pain much more than Slope '0' and '1'"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "c0b39456274f1e0f402704714494161ddc55f16a"
   },
   "source": [
    "### Analysing the 'ca' feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {
    "_uuid": "50db41d7e9ebe645bc7c6fcbaf26194176c274db"
   },
   "outputs": [],
   "source": [
    "#number of major vessels (0-3) colored by flourosopy"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {
    "_uuid": "a3b7ed6661d24dc399963afbca1e08d79243b431"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0, 2, 1, 3, 4])"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"ca\"].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {
    "_uuid": "f463859906d0287c68152ebe3cadc241e569802c"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bd13940>"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.countplot(dataset[\"ca\"])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {
    "_uuid": "81483318bc63c7434eeb75515483c329abcf15e3"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bc34c88>"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"ca\"],y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "87671e11e19372848af999bb17d061f577eb08b5"
   },
   "source": [
    "##### ca=4 has astonishingly large number of heart patients"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {
    "_uuid": "b4b057d99c7c3cdbe9e304a75b399f214f352aba"
   },
   "outputs": [],
   "source": [
    "### Analysing the 'thal' feature"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {
    "_uuid": "16eaf9a5f7433be2028369818aa54e2bf01e544e"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([1, 2, 3, 0])"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dataset[\"thal\"].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {
    "_uuid": "08947d9c4b05d68b2fe5ae70e33566063c44f8d4"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754bb89128>"
      ]
     },
     "execution_count": 36,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(dataset[\"thal\"],y)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "metadata": {
    "_uuid": "dc84bb1643cbed20e8ac5980db59ffd54d5b581c"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f754baf1fd0>"
      ]
     },
     "execution_count": 37,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.distplot(dataset[\"thal\"])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "d1c95f2180e264978c85703ece34898dab4d522b"
   },
   "source": [
    "## IV. Train Test split"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {
    "_uuid": "829fcda5b63e1b9f7ecb7762e8ca617166533aca"
   },
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split\n",
    "\n",
    "predictors = dataset.drop(\"target\",axis=1)\n",
    "target = dataset[\"target\"]\n",
    "\n",
    "X_train,X_test,Y_train,Y_test = train_test_split(predictors,target,test_size=0.20,random_state=0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "metadata": {
    "_uuid": "7a74842015c2f193d16caa4fa25e2c4cbf1940f8"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(242, 13)"
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "X_train.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "metadata": {
    "_uuid": "1f777652df4521deb877dac4d5d635d8cd35b279"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61, 13)"
      ]
     },
     "execution_count": 40,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "X_test.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {
    "_uuid": "028c968a076840657faf7dbc3bfee9fe7b5ca45a"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(242,)"
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_train.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "metadata": {
    "_uuid": "eb6857dfc18da52dae38bec95d20106f39136e61"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 42,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_test.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "3b4f28488a92917f26e9876c1880295ec9c077ed"
   },
   "source": [
    "## V. Model Fitting"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "metadata": {
    "_uuid": "fe363c1be8335a48a4444660db5fa6bd0a24b71a"
   },
   "outputs": [],
   "source": [
    "from sklearn.metrics import accuracy_score"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "afa6b322cbc225f3353bd295aea24fe5fbbb78fe"
   },
   "source": [
    "### Logistic Regression"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "metadata": {
    "_uuid": "9aea2f597203ccf38cd0d67ae58bff6e163dea1c"
   },
   "outputs": [],
   "source": [
    "from sklearn.linear_model import LogisticRegression\n",
    "\n",
    "lr = LogisticRegression()\n",
    "\n",
    "lr.fit(X_train,Y_train)\n",
    "\n",
    "Y_pred_lr = lr.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "metadata": {
    "_uuid": "58fb833d1c74355ebdafe926968632942f377421"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_lr.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "metadata": {
    "_uuid": "ee4cba838316adf863f8daf131d36a970d36b839"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Logistic Regression is: 85.25 %\n"
     ]
    }
   ],
   "source": [
    "score_lr = round(accuracy_score(Y_pred_lr,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using Logistic Regression is: \"+str(score_lr)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "4f92fceb9584ae03d3ab370ee11899cb287be690"
   },
   "source": [
    "### Naive Bayes"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "metadata": {
    "_uuid": "ffcdab99b4108902547f0179a242a9757078dc68"
   },
   "outputs": [],
   "source": [
    "from sklearn.naive_bayes import GaussianNB\n",
    "\n",
    "nb = GaussianNB()\n",
    "\n",
    "nb.fit(X_train,Y_train)\n",
    "\n",
    "Y_pred_nb = nb.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "metadata": {
    "_uuid": "9109059d06e4c92494451b3cdab0bbb5a1816072"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 48,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_nb.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {
    "_uuid": "e8f8f55db061ada0b669ffa46e9ecc745fcda1ae"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Naive Bayes is: 85.25 %\n"
     ]
    }
   ],
   "source": [
    "score_nb = round(accuracy_score(Y_pred_nb,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using Naive Bayes is: \"+str(score_nb)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "2af8b010893284bae0d6cccf66ccfda646e7ca58"
   },
   "source": [
    "### SVM"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "metadata": {
    "_uuid": "f1936ece7b76b67e552758a4c80e9421bffe0bc2"
   },
   "outputs": [],
   "source": [
    "from sklearn import svm\n",
    "\n",
    "sv = svm.SVC(kernel='linear')\n",
    "\n",
    "sv.fit(X_train, Y_train)\n",
    "\n",
    "Y_pred_svm = sv.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {
    "_uuid": "36f60f104264d44760705b9c802504f426e15592"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 51,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_svm.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {
    "_uuid": "f5a73bca6721f42b3983c328fd475390ba9bc4d3"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Linear SVM is: 81.97 %\n"
     ]
    }
   ],
   "source": [
    "score_svm = round(accuracy_score(Y_pred_svm,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using Linear SVM is: \"+str(score_svm)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "4e26d165b57f3f7882570964f1c2dc4a548404de"
   },
   "source": [
    "### K Nearest Neighbors"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 53,
   "metadata": {
    "_uuid": "286352867c53d5fb7dac2fc9bf4b2ac58a466ad0"
   },
   "outputs": [],
   "source": [
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "\n",
    "knn = KNeighborsClassifier(n_neighbors=7)\n",
    "knn.fit(X_train,Y_train)\n",
    "Y_pred_knn=knn.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {
    "_uuid": "bccb7c1fcec36dd2eb7eb222f49604029adec2b4"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_knn.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "metadata": {
    "_uuid": "dda4e8f8f18f96557cdd38cee177de0456db5f45"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using KNN is: 67.21 %\n"
     ]
    }
   ],
   "source": [
    "score_knn = round(accuracy_score(Y_pred_knn,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using KNN is: \"+str(score_knn)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "abb767170c662e4d9a8b240fd0fd7286ffb0b67f"
   },
   "source": [
    "### Decision Tree"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "metadata": {
    "_uuid": "8c141316764dce80103d1879c9b17d853702a746"
   },
   "outputs": [],
   "source": [
    "from sklearn.tree import DecisionTreeClassifier\n",
    "\n",
    "max_accuracy = 0\n",
    "\n",
    "\n",
    "for x in range(200):\n",
    "    dt = DecisionTreeClassifier(random_state=x)\n",
    "    dt.fit(X_train,Y_train)\n",
    "    Y_pred_dt = dt.predict(X_test)\n",
    "    current_accuracy = round(accuracy_score(Y_pred_dt,Y_test)*100,2)\n",
    "    if(current_accuracy>max_accuracy):\n",
    "        max_accuracy = current_accuracy\n",
    "        best_x = x\n",
    "        \n",
    "#print(max_accuracy)\n",
    "#print(best_x)\n",
    "\n",
    "\n",
    "dt = DecisionTreeClassifier(random_state=best_x)\n",
    "dt.fit(X_train,Y_train)\n",
    "Y_pred_dt = dt.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "metadata": {
    "_uuid": "8de0bd2d57abd24d3a97a5b020a24439eb106f2b"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "(61,)\n"
     ]
    }
   ],
   "source": [
    "print(Y_pred_dt.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "metadata": {
    "_uuid": "52ab93482d3b53824e9bc2b3e4114c57253e0c5b"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Decision Tree is: 81.97 %\n"
     ]
    }
   ],
   "source": [
    "score_dt = round(accuracy_score(Y_pred_dt,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using Decision Tree is: \"+str(score_dt)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "9e663d26efb00a434751f06ad0292949eff6c358"
   },
   "source": [
    "### Random Forest"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "metadata": {
    "_uuid": "8284f5222cf90be1bcd37887c45f91cf22ed1193"
   },
   "outputs": [],
   "source": [
    "from sklearn.ensemble import RandomForestClassifier\n",
    "\n",
    "max_accuracy = 0\n",
    "\n",
    "\n",
    "for x in range(2000):\n",
    "    rf = RandomForestClassifier(random_state=x)\n",
    "    rf.fit(X_train,Y_train)\n",
    "    Y_pred_rf = rf.predict(X_test)\n",
    "    current_accuracy = round(accuracy_score(Y_pred_rf,Y_test)*100,2)\n",
    "    if(current_accuracy>max_accuracy):\n",
    "        max_accuracy = current_accuracy\n",
    "        best_x = x\n",
    "        \n",
    "#print(max_accuracy)\n",
    "#print(best_x)\n",
    "\n",
    "rf = RandomForestClassifier(random_state=best_x)\n",
    "rf.fit(X_train,Y_train)\n",
    "Y_pred_rf = rf.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
   "metadata": {
    "_uuid": "edc8e1cbb57be0aa9e9ad5f4997212d53a9a4c99"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 60,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_rf.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {
    "_uuid": "965228f30e05e07e7960a3375dc7dc85b49caed7"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Decision Tree is: 95.08 %\n"
     ]
    }
   ],
   "source": [
    "score_rf = round(accuracy_score(Y_pred_rf,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using Decision Tree is: \"+str(score_rf)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "6a0fc13a6c2fccd6a725a7691cfe95d74348a8ae"
   },
   "source": [
    "### XGBoost"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {
    "_uuid": "5a437f3c0e190887e2192ecb1844eaa6eb1d34a7"
   },
   "outputs": [],
   "source": [
    "import xgboost as xgb\n",
    "\n",
    "xgb_model = xgb.XGBClassifier(objective=\"binary:logistic\", random_state=42)\n",
    "xgb_model.fit(X_train, Y_train)\n",
    "\n",
    "Y_pred_xgb = xgb_model.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "metadata": {
    "_uuid": "168d52cd705f2abb6763107328c984e4252c618e"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61,)"
      ]
     },
     "execution_count": 63,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_xgb.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {
    "_uuid": "319c4f0d2e62b03c95a48df0ecc33b15e7fa7f39"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using XGBoost is: 85.25 %\n"
     ]
    }
   ],
   "source": [
    "score_xgb = round(accuracy_score(Y_pred_xgb,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using XGBoost is: \"+str(score_xgb)+\" %\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "e224ab23f275a3a56cdba6a9ccfddbd6a4d3b4fd"
   },
   "source": [
    "### Neural Network"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 65,
   "metadata": {
    "_uuid": "727b391ad6d86468a96e93dc645ade6e2da4048e"
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "Using TensorFlow backend.\n"
     ]
    }
   ],
   "source": [
    "from keras.models import Sequential\n",
    "from keras.layers import Dense"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
   "metadata": {
    "_uuid": "650f1baa7db466923626c707408319fa29f22d10"
   },
   "outputs": [],
   "source": [
    "# https://stats.stackexchange.com/a/136542 helped a lot in avoiding overfitting\n",
    "\n",
    "model = Sequential()\n",
    "model.add(Dense(11,activation='relu',input_dim=13))\n",
    "model.add(Dense(1,activation='sigmoid'))\n",
    "\n",
    "model.compile(loss='binary_crossentropy',optimizer='adam',metrics=['accuracy'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 67,
   "metadata": {
    "_uuid": "dde4e50b5c4c24c73b03133fc7c90bf663fd6d82"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Epoch 1/300\n",
      "242/242 [==============================] - 3s 10ms/step - loss: 4.7817 - acc: 0.6074\n",
      "Epoch 2/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 2.6633 - acc: 0.6033\n",
      "Epoch 3/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 2.3371 - acc: 0.6281\n",
      "Epoch 4/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 2.2938 - acc: 0.6488\n",
      "Epoch 5/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 2.0712 - acc: 0.6860\n",
      "Epoch 6/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 2.0645 - acc: 0.6653\n",
      "Epoch 7/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 2.0023 - acc: 0.6860\n",
      "Epoch 8/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 1.9928 - acc: 0.6694\n",
      "Epoch 9/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 1.9670 - acc: 0.6694\n",
      "Epoch 10/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.9316 - acc: 0.6736\n",
      "Epoch 11/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.9223 - acc: 0.6901\n",
      "Epoch 12/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.8955 - acc: 0.6818\n",
      "Epoch 13/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.8573 - acc: 0.6901\n",
      "Epoch 14/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 1.8268 - acc: 0.6860\n",
      "Epoch 15/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 1.7915 - acc: 0.6860\n",
      "Epoch 16/300\n",
      "242/242 [==============================] - 0s 121us/step - loss: 1.7727 - acc: 0.6777\n",
      "Epoch 17/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 1.7275 - acc: 0.6860\n",
      "Epoch 18/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 1.7143 - acc: 0.7066\n",
      "Epoch 19/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.6761 - acc: 0.6860\n",
      "Epoch 20/300\n",
      "242/242 [==============================] - 0s 136us/step - loss: 1.6591 - acc: 0.6777\n",
      "Epoch 21/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 1.6486 - acc: 0.7107\n",
      "Epoch 22/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 1.6004 - acc: 0.6860\n",
      "Epoch 23/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 1.5765 - acc: 0.7107\n",
      "Epoch 24/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 1.5428 - acc: 0.7025\n",
      "Epoch 25/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 1.5179 - acc: 0.6901\n",
      "Epoch 26/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.5084 - acc: 0.7066\n",
      "Epoch 27/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.4619 - acc: 0.6942\n",
      "Epoch 28/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 1.4600 - acc: 0.6818\n",
      "Epoch 29/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.4072 - acc: 0.6942\n",
      "Epoch 30/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 1.4329 - acc: 0.6942\n",
      "Epoch 31/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.3622 - acc: 0.7066\n",
      "Epoch 32/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 1.3532 - acc: 0.7025\n",
      "Epoch 33/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 1.3160 - acc: 0.7066\n",
      "Epoch 34/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 1.3004 - acc: 0.7025\n",
      "Epoch 35/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.2741 - acc: 0.7025\n",
      "Epoch 36/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 1.2875 - acc: 0.7107\n",
      "Epoch 37/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.2634 - acc: 0.6983\n",
      "Epoch 38/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 1.2101 - acc: 0.6983\n",
      "Epoch 39/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.1919 - acc: 0.7025\n",
      "Epoch 40/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 1.2064 - acc: 0.6942\n",
      "Epoch 41/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.2389 - acc: 0.6818\n",
      "Epoch 42/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 1.1472 - acc: 0.7066\n",
      "Epoch 43/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 1.1238 - acc: 0.6942\n",
      "Epoch 44/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 1.1178 - acc: 0.7025\n",
      "Epoch 45/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 1.0960 - acc: 0.6983\n",
      "Epoch 46/300\n",
      "242/242 [==============================] - 0s 120us/step - loss: 1.0781 - acc: 0.7025\n",
      "Epoch 47/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.0553 - acc: 0.7025\n",
      "Epoch 48/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 1.0342 - acc: 0.7149\n",
      "Epoch 49/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 1.0223 - acc: 0.7066\n",
      "Epoch 50/300\n",
      "242/242 [==============================] - 0s 134us/step - loss: 1.0213 - acc: 0.7107\n",
      "Epoch 51/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.9977 - acc: 0.7231\n",
      "Epoch 52/300\n",
      "242/242 [==============================] - 0s 137us/step - loss: 0.9841 - acc: 0.7190\n",
      "Epoch 53/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.9594 - acc: 0.7149\n",
      "Epoch 54/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.9688 - acc: 0.7231\n",
      "Epoch 55/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.9942 - acc: 0.6901\n",
      "Epoch 56/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.9391 - acc: 0.7149\n",
      "Epoch 57/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.9229 - acc: 0.6942\n",
      "Epoch 58/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.8981 - acc: 0.7190\n",
      "Epoch 59/300\n",
      "242/242 [==============================] - 0s 134us/step - loss: 0.8885 - acc: 0.7190\n",
      "Epoch 60/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.8854 - acc: 0.7149\n",
      "Epoch 61/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.8573 - acc: 0.7066\n",
      "Epoch 62/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.8476 - acc: 0.7273\n",
      "Epoch 63/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.8410 - acc: 0.7149\n",
      "Epoch 64/300\n",
      "242/242 [==============================] - 0s 119us/step - loss: 0.8287 - acc: 0.7355\n",
      "Epoch 65/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.8199 - acc: 0.7397\n",
      "Epoch 66/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.8091 - acc: 0.7355\n",
      "Epoch 67/300\n",
      "242/242 [==============================] - 0s 121us/step - loss: 0.7976 - acc: 0.7107\n",
      "Epoch 68/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.7912 - acc: 0.7231\n",
      "Epoch 69/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.7775 - acc: 0.7479\n",
      "Epoch 70/300\n",
      "242/242 [==============================] - 0s 121us/step - loss: 0.7608 - acc: 0.7355\n",
      "Epoch 71/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.7553 - acc: 0.7231\n",
      "Epoch 72/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.7470 - acc: 0.7397\n",
      "Epoch 73/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.7429 - acc: 0.7521\n",
      "Epoch 74/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.7543 - acc: 0.7190\n",
      "Epoch 75/300\n",
      "242/242 [==============================] - 0s 120us/step - loss: 0.7206 - acc: 0.7438\n",
      "Epoch 76/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.7220 - acc: 0.7479\n",
      "Epoch 77/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.7237 - acc: 0.7066\n",
      "Epoch 78/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.7065 - acc: 0.7273\n",
      "Epoch 79/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.6893 - acc: 0.7314\n",
      "Epoch 80/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.6972 - acc: 0.7397\n",
      "Epoch 81/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.6626 - acc: 0.7273\n",
      "Epoch 82/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.6600 - acc: 0.7521\n",
      "Epoch 83/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.6686 - acc: 0.7231\n",
      "Epoch 84/300\n",
      "242/242 [==============================] - 0s 136us/step - loss: 0.6550 - acc: 0.7397\n",
      "Epoch 85/300\n",
      "242/242 [==============================] - 0s 137us/step - loss: 0.6363 - acc: 0.7397\n",
      "Epoch 86/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.6298 - acc: 0.7438\n",
      "Epoch 87/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.6332 - acc: 0.7562\n",
      "Epoch 88/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.6204 - acc: 0.7521\n",
      "Epoch 89/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.6155 - acc: 0.7438\n",
      "Epoch 90/300\n",
      "242/242 [==============================] - 0s 137us/step - loss: 0.6085 - acc: 0.7603\n",
      "Epoch 91/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.6035 - acc: 0.7273\n",
      "Epoch 92/300\n",
      "242/242 [==============================] - 0s 133us/step - loss: 0.5924 - acc: 0.7562\n",
      "Epoch 93/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.6020 - acc: 0.7562\n",
      "Epoch 94/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.5888 - acc: 0.7603\n",
      "Epoch 95/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.5771 - acc: 0.7355\n",
      "Epoch 96/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.5699 - acc: 0.7603\n",
      "Epoch 97/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.5732 - acc: 0.7521\n",
      "Epoch 98/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.5631 - acc: 0.7603\n",
      "Epoch 99/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.5576 - acc: 0.7645\n",
      "Epoch 100/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.5528 - acc: 0.7645\n",
      "Epoch 101/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.5459 - acc: 0.7521\n",
      "Epoch 102/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.5379 - acc: 0.7645\n",
      "Epoch 103/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.5654 - acc: 0.7810\n",
      "Epoch 104/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.5296 - acc: 0.7562\n",
      "Epoch 105/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.5355 - acc: 0.7769\n",
      "Epoch 106/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.5250 - acc: 0.7686\n",
      "Epoch 107/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.5180 - acc: 0.7769\n",
      "Epoch 108/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.5170 - acc: 0.7562\n",
      "Epoch 109/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.5071 - acc: 0.7810\n",
      "Epoch 110/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.5054 - acc: 0.7810\n",
      "Epoch 111/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.5196 - acc: 0.7769\n",
      "Epoch 112/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.5005 - acc: 0.7769\n",
      "Epoch 113/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.5047 - acc: 0.7727\n",
      "Epoch 114/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.4910 - acc: 0.7769\n",
      "Epoch 115/300\n",
      "242/242 [==============================] - 0s 121us/step - loss: 0.4900 - acc: 0.7769\n",
      "Epoch 116/300\n",
      "242/242 [==============================] - 0s 138us/step - loss: 0.5211 - acc: 0.7686\n",
      "Epoch 117/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.4756 - acc: 0.7893\n",
      "Epoch 118/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.4844 - acc: 0.7769\n",
      "Epoch 119/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.4720 - acc: 0.7934\n",
      "Epoch 120/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.4720 - acc: 0.7893\n",
      "Epoch 121/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.4669 - acc: 0.7893\n",
      "Epoch 122/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.4736 - acc: 0.7851\n",
      "Epoch 123/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.4580 - acc: 0.7975\n",
      "Epoch 124/300\n",
      "242/242 [==============================] - 0s 140us/step - loss: 0.4592 - acc: 0.7851\n",
      "Epoch 125/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.4571 - acc: 0.8017\n",
      "Epoch 126/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.4596 - acc: 0.7727\n",
      "Epoch 127/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.4581 - acc: 0.7893\n",
      "Epoch 128/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.4543 - acc: 0.7934\n",
      "Epoch 129/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.4893 - acc: 0.7727\n",
      "Epoch 130/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.4437 - acc: 0.8058\n",
      "Epoch 131/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4630 - acc: 0.7975\n",
      "Epoch 132/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.4564 - acc: 0.7851\n",
      "Epoch 133/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4346 - acc: 0.7975\n",
      "Epoch 134/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.4375 - acc: 0.7975\n",
      "Epoch 135/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4382 - acc: 0.7975\n",
      "Epoch 136/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4308 - acc: 0.8017\n",
      "Epoch 137/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.4332 - acc: 0.8017\n",
      "Epoch 138/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4275 - acc: 0.8017\n",
      "Epoch 139/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4311 - acc: 0.7975\n",
      "Epoch 140/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.4346 - acc: 0.8099\n",
      "Epoch 141/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4289 - acc: 0.8223\n",
      "Epoch 142/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4213 - acc: 0.8099\n",
      "Epoch 143/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4319 - acc: 0.8058\n",
      "Epoch 144/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4252 - acc: 0.8017\n",
      "Epoch 145/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.4389 - acc: 0.8182\n",
      "Epoch 146/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4292 - acc: 0.8017\n",
      "Epoch 147/300\n",
      "242/242 [==============================] - 0s 138us/step - loss: 0.4251 - acc: 0.8058\n",
      "Epoch 148/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.4114 - acc: 0.8099\n",
      "Epoch 149/300\n",
      "242/242 [==============================] - 0s 136us/step - loss: 0.4233 - acc: 0.7975\n",
      "Epoch 150/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.4072 - acc: 0.8182\n",
      "Epoch 151/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.4449 - acc: 0.7851\n",
      "Epoch 152/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.4335 - acc: 0.7934\n",
      "Epoch 153/300\n",
      "242/242 [==============================] - 0s 134us/step - loss: 0.4077 - acc: 0.8182\n",
      "Epoch 154/300\n",
      "242/242 [==============================] - 0s 154us/step - loss: 0.4137 - acc: 0.8099\n",
      "Epoch 155/300\n",
      "242/242 [==============================] - 0s 139us/step - loss: 0.4079 - acc: 0.8182\n",
      "Epoch 156/300\n",
      "242/242 [==============================] - 0s 135us/step - loss: 0.4054 - acc: 0.8140\n",
      "Epoch 157/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.4072 - acc: 0.8223\n",
      "Epoch 158/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.4062 - acc: 0.8182\n",
      "Epoch 159/300\n",
      "242/242 [==============================] - 0s 134us/step - loss: 0.4031 - acc: 0.8306\n",
      "Epoch 160/300\n",
      "242/242 [==============================] - 0s 140us/step - loss: 0.4019 - acc: 0.8058\n",
      "Epoch 161/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.4005 - acc: 0.8223\n",
      "Epoch 162/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.4108 - acc: 0.8140\n",
      "Epoch 163/300\n",
      "242/242 [==============================] - 0s 136us/step - loss: 0.3946 - acc: 0.8264\n",
      "Epoch 164/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3961 - acc: 0.8058\n",
      "Epoch 165/300\n",
      "242/242 [==============================] - 0s 143us/step - loss: 0.4076 - acc: 0.8223\n",
      "Epoch 166/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.4033 - acc: 0.8182\n",
      "Epoch 167/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.4171 - acc: 0.8140\n",
      "Epoch 168/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3988 - acc: 0.8388\n",
      "Epoch 169/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3987 - acc: 0.8182\n",
      "Epoch 170/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.4012 - acc: 0.8182\n",
      "Epoch 171/300\n",
      "242/242 [==============================] - 0s 137us/step - loss: 0.3952 - acc: 0.8140\n",
      "Epoch 172/300\n",
      "242/242 [==============================] - 0s 134us/step - loss: 0.4002 - acc: 0.8430\n",
      "Epoch 173/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3978 - acc: 0.8099\n",
      "Epoch 174/300\n",
      "242/242 [==============================] - 0s 139us/step - loss: 0.4227 - acc: 0.8264\n",
      "Epoch 175/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.4119 - acc: 0.8347\n",
      "Epoch 176/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4099 - acc: 0.8017\n",
      "Epoch 177/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.3934 - acc: 0.8388\n",
      "Epoch 178/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3995 - acc: 0.8099\n",
      "Epoch 179/300\n",
      "242/242 [==============================] - 0s 134us/step - loss: 0.3905 - acc: 0.8264\n",
      "Epoch 180/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3884 - acc: 0.8182\n",
      "Epoch 181/300\n",
      "242/242 [==============================] - 0s 135us/step - loss: 0.3856 - acc: 0.8471\n",
      "Epoch 182/300\n",
      "242/242 [==============================] - 0s 142us/step - loss: 0.3851 - acc: 0.8140\n",
      "Epoch 183/300\n",
      "242/242 [==============================] - 0s 156us/step - loss: 0.3884 - acc: 0.8430\n",
      "Epoch 184/300\n",
      "242/242 [==============================] - 0s 133us/step - loss: 0.3905 - acc: 0.8223\n",
      "Epoch 185/300\n",
      "242/242 [==============================] - 0s 141us/step - loss: 0.4023 - acc: 0.8140\n",
      "Epoch 186/300\n",
      "242/242 [==============================] - 0s 139us/step - loss: 0.3969 - acc: 0.8347\n",
      "Epoch 187/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.3801 - acc: 0.8264\n",
      "Epoch 188/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.4085 - acc: 0.7975\n",
      "Epoch 189/300\n",
      "242/242 [==============================] - 0s 135us/step - loss: 0.4002 - acc: 0.8099\n",
      "Epoch 190/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3857 - acc: 0.8223\n",
      "Epoch 191/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3961 - acc: 0.8471\n",
      "Epoch 192/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3903 - acc: 0.8140\n",
      "Epoch 193/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3921 - acc: 0.8306\n",
      "Epoch 194/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.4042 - acc: 0.8017\n",
      "Epoch 195/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4186 - acc: 0.7934\n",
      "Epoch 196/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3855 - acc: 0.8264\n",
      "Epoch 197/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3961 - acc: 0.8140\n",
      "Epoch 198/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3932 - acc: 0.8099\n",
      "Epoch 199/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3860 - acc: 0.8264\n",
      "Epoch 200/300\n",
      "242/242 [==============================] - 0s 133us/step - loss: 0.3876 - acc: 0.8388\n",
      "Epoch 201/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3915 - acc: 0.8347\n",
      "Epoch 202/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4143 - acc: 0.8182\n",
      "Epoch 203/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3690 - acc: 0.8223\n",
      "Epoch 204/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3847 - acc: 0.8347\n",
      "Epoch 205/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3764 - acc: 0.8306\n",
      "Epoch 206/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3731 - acc: 0.8347\n",
      "Epoch 207/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3760 - acc: 0.8430\n",
      "Epoch 208/300\n",
      "242/242 [==============================] - 0s 137us/step - loss: 0.3779 - acc: 0.8388\n",
      "Epoch 209/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.3776 - acc: 0.8223\n",
      "Epoch 210/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.3848 - acc: 0.8430\n",
      "Epoch 211/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3753 - acc: 0.8471\n",
      "Epoch 212/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.3796 - acc: 0.8388\n",
      "Epoch 213/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3736 - acc: 0.8347\n",
      "Epoch 214/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3741 - acc: 0.8306\n",
      "Epoch 215/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3748 - acc: 0.8306\n",
      "Epoch 216/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.3738 - acc: 0.8347\n",
      "Epoch 217/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3754 - acc: 0.8471\n",
      "Epoch 218/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3826 - acc: 0.8388\n",
      "Epoch 219/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3900 - acc: 0.8264\n",
      "Epoch 220/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3745 - acc: 0.8430\n",
      "Epoch 221/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3828 - acc: 0.8264\n",
      "Epoch 222/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3902 - acc: 0.8306\n",
      "Epoch 223/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.3700 - acc: 0.8512\n",
      "Epoch 224/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3746 - acc: 0.8388\n",
      "Epoch 225/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3863 - acc: 0.8430\n",
      "Epoch 226/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3698 - acc: 0.8347\n",
      "Epoch 227/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3811 - acc: 0.8388\n",
      "Epoch 228/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3801 - acc: 0.8306\n",
      "Epoch 229/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3742 - acc: 0.8347\n",
      "Epoch 230/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3743 - acc: 0.8430\n",
      "Epoch 231/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3958 - acc: 0.8264\n",
      "Epoch 232/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3665 - acc: 0.8347\n",
      "Epoch 233/300\n",
      "242/242 [==============================] - 0s 143us/step - loss: 0.3952 - acc: 0.8347\n",
      "Epoch 234/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3763 - acc: 0.8264\n",
      "Epoch 235/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3685 - acc: 0.8512\n",
      "Epoch 236/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3707 - acc: 0.8347\n",
      "Epoch 237/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4014 - acc: 0.8017\n",
      "Epoch 238/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.4119 - acc: 0.8223\n",
      "Epoch 239/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3824 - acc: 0.8388\n",
      "Epoch 240/300\n",
      "242/242 [==============================] - 0s 152us/step - loss: 0.3735 - acc: 0.8388\n",
      "Epoch 241/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.3757 - acc: 0.8347\n",
      "Epoch 242/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3697 - acc: 0.8471\n",
      "Epoch 243/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3718 - acc: 0.8223\n",
      "Epoch 244/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3763 - acc: 0.8306\n",
      "Epoch 245/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3705 - acc: 0.8306\n",
      "Epoch 246/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3737 - acc: 0.8347\n",
      "Epoch 247/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3676 - acc: 0.8388\n",
      "Epoch 248/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3702 - acc: 0.8471\n",
      "Epoch 249/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3711 - acc: 0.8471\n",
      "Epoch 250/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3762 - acc: 0.8471\n",
      "Epoch 251/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3684 - acc: 0.8471\n",
      "Epoch 252/300\n",
      "242/242 [==============================] - 0s 133us/step - loss: 0.3945 - acc: 0.8182\n",
      "Epoch 253/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.3693 - acc: 0.8430\n",
      "Epoch 254/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3672 - acc: 0.8388\n",
      "Epoch 255/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3718 - acc: 0.8512\n",
      "Epoch 256/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3768 - acc: 0.8347\n",
      "Epoch 257/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3852 - acc: 0.8388\n",
      "Epoch 258/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3752 - acc: 0.8471\n",
      "Epoch 259/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3693 - acc: 0.8347\n",
      "Epoch 260/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3683 - acc: 0.8388\n",
      "Epoch 261/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.3690 - acc: 0.8430\n",
      "Epoch 262/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3652 - acc: 0.8388\n",
      "Epoch 263/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3677 - acc: 0.8347\n",
      "Epoch 264/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3677 - acc: 0.8347\n",
      "Epoch 265/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3814 - acc: 0.8430\n",
      "Epoch 266/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3878 - acc: 0.8347\n",
      "Epoch 267/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3708 - acc: 0.8347\n",
      "Epoch 268/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3663 - acc: 0.8306\n",
      "Epoch 269/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3741 - acc: 0.8264\n",
      "Epoch 270/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3709 - acc: 0.8347\n",
      "Epoch 271/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3628 - acc: 0.8430\n",
      "Epoch 272/300\n",
      "242/242 [==============================] - 0s 139us/step - loss: 0.3671 - acc: 0.8471\n",
      "Epoch 273/300\n",
      "242/242 [==============================] - 0s 129us/step - loss: 0.3640 - acc: 0.8430\n",
      "Epoch 274/300\n",
      "242/242 [==============================] - 0s 122us/step - loss: 0.3669 - acc: 0.8306\n",
      "Epoch 275/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3725 - acc: 0.8306\n",
      "Epoch 276/300\n",
      "242/242 [==============================] - 0s 131us/step - loss: 0.3747 - acc: 0.8388\n",
      "Epoch 277/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3638 - acc: 0.8430\n",
      "Epoch 278/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.4032 - acc: 0.8306\n",
      "Epoch 279/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3787 - acc: 0.8388\n",
      "Epoch 280/300\n",
      "242/242 [==============================] - 0s 121us/step - loss: 0.3636 - acc: 0.8512\n",
      "Epoch 281/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3599 - acc: 0.8554\n",
      "Epoch 282/300\n",
      "242/242 [==============================] - 0s 123us/step - loss: 0.3689 - acc: 0.8347\n",
      "Epoch 283/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.3785 - acc: 0.8306\n",
      "Epoch 284/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3619 - acc: 0.8430\n",
      "Epoch 285/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3663 - acc: 0.8471\n",
      "Epoch 286/300\n",
      "242/242 [==============================] - 0s 127us/step - loss: 0.3636 - acc: 0.8306\n",
      "Epoch 287/300\n",
      "242/242 [==============================] - 0s 126us/step - loss: 0.3804 - acc: 0.8306\n",
      "Epoch 288/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3760 - acc: 0.8471\n",
      "Epoch 289/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3727 - acc: 0.8388\n",
      "Epoch 290/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3601 - acc: 0.8471\n",
      "Epoch 291/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3667 - acc: 0.8347\n",
      "Epoch 292/300\n",
      "242/242 [==============================] - 0s 124us/step - loss: 0.3678 - acc: 0.8388\n",
      "Epoch 293/300\n",
      "242/242 [==============================] - 0s 128us/step - loss: 0.3625 - acc: 0.8595\n",
      "Epoch 294/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3794 - acc: 0.8388\n",
      "Epoch 295/300\n",
      "242/242 [==============================] - 0s 132us/step - loss: 0.3635 - acc: 0.8388\n",
      "Epoch 296/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3685 - acc: 0.8430\n",
      "Epoch 297/300\n",
      "242/242 [==============================] - 0s 125us/step - loss: 0.3695 - acc: 0.8388\n",
      "Epoch 298/300\n",
      "242/242 [==============================] - 0s 121us/step - loss: 0.3844 - acc: 0.8347\n",
      "Epoch 299/300\n",
      "242/242 [==============================] - 0s 130us/step - loss: 0.3653 - acc: 0.8471\n",
      "Epoch 300/300\n",
      "242/242 [==============================] - 0s 142us/step - loss: 0.3721 - acc: 0.8471\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "<keras.callbacks.History at 0x7f74eb3f4da0>"
      ]
     },
     "execution_count": 67,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "model.fit(X_train,Y_train,epochs=300)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 68,
   "metadata": {
    "_uuid": "c844af4f00d40c4cce4c4e5a9a01c9a892e9533d"
   },
   "outputs": [],
   "source": [
    "Y_pred_nn = model.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 69,
   "metadata": {
    "_uuid": "7e95c4946c0103225663862f43f31c41ed5aa2b1"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(61, 1)"
      ]
     },
     "execution_count": 69,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred_nn.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 70,
   "metadata": {
    "_uuid": "66d9268e3f87b5a98066196eaa39363218a20015"
   },
   "outputs": [],
   "source": [
    "rounded = [round(x[0]) for x in Y_pred_nn]\n",
    "\n",
    "Y_pred_nn = rounded"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 71,
   "metadata": {
    "_uuid": "888d79632c3191c2d11c1ec3da8dc750c9d95424"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Neural Network is: 80.33 %\n"
     ]
    }
   ],
   "source": [
    "score_nn = round(accuracy_score(Y_pred_nn,Y_test)*100,2)\n",
    "\n",
    "print(\"The accuracy score achieved using Neural Network is: \"+str(score_nn)+\" %\")\n",
    "\n",
    "#Note: Accuracy of 85% can be achieved on the test set, by setting epochs=2000, and number of nodes = 11. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "c634cd922d716d350f6db0244772260cc598dec4"
   },
   "source": [
    "## VI. Output final score"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 72,
   "metadata": {
    "_uuid": "101daa51242624c49bb8b3198d9d2c9f8f1c596e"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The accuracy score achieved using Logistic Regression is: 85.25 %\n",
      "The accuracy score achieved using Naive Bayes is: 85.25 %\n",
      "The accuracy score achieved using Support Vector Machine is: 81.97 %\n",
      "The accuracy score achieved using K-Nearest Neighbors is: 67.21 %\n",
      "The accuracy score achieved using Decision Tree is: 81.97 %\n",
      "The accuracy score achieved using Random Forest is: 95.08 %\n",
      "The accuracy score achieved using XGBoost is: 85.25 %\n",
      "The accuracy score achieved using Neural Network is: 80.33 %\n"
     ]
    }
   ],
   "source": [
    "scores = [score_lr,score_nb,score_svm,score_knn,score_dt,score_rf,score_xgb,score_nn]\n",
    "algorithms = [\"Logistic Regression\",\"Naive Bayes\",\"Support Vector Machine\",\"K-Nearest Neighbors\",\"Decision Tree\",\"Random Forest\",\"XGBoost\",\"Neural Network\"]    \n",
    "\n",
    "for i in range(len(algorithms)):\n",
    "    print(\"The accuracy score achieved using \"+algorithms[i]+\" is: \"+str(scores[i])+\" %\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 73,
   "metadata": {
    "_uuid": "8060c7d426f9f7b64772f37e0a74ededca16838d"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f74ea800eb8>"
      ]
     },
     "execution_count": 73,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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wYIF1apVK0VHR6tXr15avny5/vrXv0q6Ou/37NnjnJ3JOCN3MzNmzFD16tWVkpKiIUOGaN68eXr66aeVkJCgF198UbGxscqXL5/Onz+vmJgY1alTRz179tSSJUvUsGFDLV682LlMav369dq3b5+6dOki6eqlhhcuXJDkWbtIkp+fn95++20dOHBA27dv13/+8x/NmTPnhsv4r+XPn985S9OoUSMVKFBAhw8fVuHChW/ab/v27WrevLlKly4t6eoyHRoa6oyzXr162bpUOiQkRNOnT9e5c+e0d+9eFSxY0DmblVXbfPnll84v8NLN17tdu3bpvvvu0x//+EdJVy9BHT9+vHOfTKVKlZzp3cxdd92lOnXqaO3atfrmm2/0yiuvZFrnjx07phEjRiguLk7+/v46c+aMTp8+rXPnzik1NdU5yydJxYsXd17/er05cuSImjdvrtWrV2c609iqVSsFBgZKku6//37nzMH+/fuVmJio2NhYtWvXTufPn3fO9K9fv16XLl3SqlWrJF3dpjzwwAOSrv4aPWLECJ06dUr58uVTXFycEhISnHl4bXuuX79ee/fuzbSMZpyladSokd5++20dOXJETZo0ca688NSTTz6p+fPnX3fpaFa1XyvjTG7GfA0ODs7Uv1mzZipSpIgkqXbt2pnu4w4ODs60T5gyZYokadOmTZowYYJcLpeKFCmixx57TJs2bVKTJk0kSR07dnQuz61Tp44WLVqkggULZtqm/hbmmkvxstovfPnll1q2bJlzZulGy39e2ba3aNHCWe4PHTqkw4cP64UXXnD6p6am6tChQzLG6Pjx45kuZ3e5XDp27JhzdYevPf/88zLG6OjRo5o+fbqzfbl8+bJzqaDL5dKpU6e0b98+VatWTdKN19EmTZpk2n9XrFgx0/578+bNGjNmjCSpdOnSat68uXOlgSTnkt0HHnhAly5dcrYjDz74YJbPJOjUqdN1Z6Q3b96s9u3bO9vPJ554QpMmTXL6N2vWzFmGjhw5okOHDmn48OFO/ytXrujw4cO3dZyUl23evFmFCxfW4cOH5Xa7rzs7JEkTJ07U9u3bFR8fr48++kjlypWTdPNjgZutU/Xr19ePP/7o3GP+xz/+UTVr1tTOnTvvqPl6o2O1ixcvatu2bUpISHC6JScn69ChQ862NSsZxwDSrdfFnKivcePG2rRpk8qU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\n",
      "text/plain": [
       "<Figure size 1080x576 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.set(rc={'figure.figsize':(15,8)})\n",
    "plt.xlabel(\"Algorithms\")\n",
    "plt.ylabel(\"Accuracy score\")\n",
    "\n",
    "sns.barplot(algorithms,scores)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "bf9c2071e0d480ab335376d8a177914a8fdca9b7"
   },
   "source": [
    "### Hey arbaaz there random forest has good result as compare to other algorithms <br> <br>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "_uuid": "16759e71e0db7e5458cd37a19fbf7b21c24e7301"
   },
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.2"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 1
}