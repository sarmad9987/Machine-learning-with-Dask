{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "7e20ae67",
   "metadata": {},
   "source": [
    "## Speedup Machine Learning using Dask Dataframe "
   ]
  },
  {
   "attachments": {
    "Screenshot%202022-02-13%20032217.jpg": {
     "image/jpeg": "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"
    }
   },
   "cell_type": "markdown",
   "id": "a7068aa6",
   "metadata": {},
   "source": [
    "#### Dask is a flexible library for parallel computing in Python. A Dask DataFrame is a large parallel DataFrame composed of many smaller Pandas DataFrames, split along the index. These Pandas DataFrames may live on disk for larger-than-memory computing on a single machine, or on many different machines in a cluster. One Dask DataFrame operation triggers many operations on the constituent Pandas DataFrames.\n",
    "![Screenshot%202022-02-13%20032217.jpg](attachment:Screenshot%202022-02-13%20032217.jpg)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f650a15c",
   "metadata": {},
   "source": [
    "**REFERENCES**\n",
    "1. https://docs.dask.org/en/stable/\n",
    "2. https://ml.dask.org/xgboost.html\n",
    "3. https://docs.dask.org/en/stable/dataframe.html\n",
    "4. https://xgboost.readthedocs.io/en/stable/get_started.html"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "cd0ec003",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table style=\"border: 2px solid white;\">\n",
       "<tr>\n",
       "<td style=\"vertical-align: top; border: 0px solid white\">\n",
       "<h3 style=\"text-align: left;\">Client</h3>\n",
       "<ul style=\"text-align: left; list-style: none; margin: 0; padding: 0;\">\n",
       "  <li><b>Scheduler: </b>tcp://127.0.0.1:51761</li>\n",
       "  <li><b>Dashboard: </b><a href='http://127.0.0.1:8787/status' target='_blank'>http://127.0.0.1:8787/status</a></li>\n",
       "</ul>\n",
       "</td>\n",
       "<td style=\"vertical-align: top; border: 0px solid white\">\n",
       "<h3 style=\"text-align: left;\">Cluster</h3>\n",
       "<ul style=\"text-align: left; list-style:none; margin: 0; padding: 0;\">\n",
       "  <li><b>Workers: </b>4</li>\n",
       "  <li><b>Cores: </b>12</li>\n",
       "  <li><b>Memory: </b>15.85 GiB</li>\n",
       "</ul>\n",
       "</td>\n",
       "</tr>\n",
       "</table>"
      ],
      "text/plain": [
       "<Client: 'tcp://127.0.0.1:51761' processes=4 threads=12, memory=15.85 GiB>"
      ]
     },
     "execution_count": 1,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import numpy as np\n",
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "from dask.distributed import Client\n",
    "from dask_ml.preprocessing import OneHotEncoder\n",
    "import dask.dataframe as dd\n",
    "import dask\n",
    "import time\n",
    "client = Client()\n",
    "client"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d108943b",
   "metadata": {},
   "source": [
    "### Read Data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "3347efa9",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "----------------------------------\n",
      " | Dask Time:  0.01996922492980957 seconds |\n",
      "----------------------------------\n"
     ]
    }
   ],
   "source": [
    "start_time = time.time()\n",
    "dd_csv=dd.read_csv('2020_taxi_trips - Copy.csv',assume_missing=True)\n",
    "print(\"----------------------------------\")\n",
    "print(\" | Dask Time:  %s seconds |\" % (time.time() - start_time))\n",
    "print(\"----------------------------------\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "75f5ef04",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "----------------------------------\n",
      " | Pandas Time:  0.697197437286377 seconds |\n",
      "----------------------------------\n"
     ]
    }
   ],
   "source": [
    "start_time = time.time()\n",
    "data = pd.read_csv('2020_taxi_trips - Copy.csv')\n",
    "print(\"----------------------------------\")\n",
    "print(\" | Pandas Time:  %s seconds |\" % (time.time() - start_time))\n",
    "print(\"----------------------------------\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "c5c98966",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 998 µs\n"
     ]
    },
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
       "      <th>VendorID</th>\n",
       "      <th>RatecodeID</th>\n",
       "      <th>PULocationID</th>\n",
       "      <th>DOLocationID</th>\n",
       "      <th>passenger_count</th>\n",
       "      <th>trip_distance</th>\n",
       "      <th>fare_amount</th>\n",
       "      <th>extra</th>\n",
       "      <th>mta_tax</th>\n",
       "      <th>tip_amount</th>\n",
       "      <th>tolls_amount</th>\n",
       "      <th>improvement_surcharge</th>\n",
       "      <th>total_amount</th>\n",
       "      <th>payment_type</th>\n",
       "      <th>trip_type</th>\n",
       "      <th>congestion_surcharge</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.47</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.3</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.49</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.3</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   VendorID  RatecodeID  PULocationID  DOLocationID  passenger_count  \\\n",
       "0       2.0         1.0          74.0          75.0              1.0   \n",
       "1       2.0         1.0          74.0          75.0              1.0   \n",
       "\n",
       "   trip_distance  fare_amount  extra  mta_tax  tip_amount  tolls_amount  \\\n",
       "0           1.47          6.5    0.0      0.5         0.0           0.0   \n",
       "1           1.49          6.5    0.0      0.5         0.0           0.0   \n",
       "\n",
       "   improvement_surcharge  total_amount  payment_type  trip_type  \\\n",
       "0                    0.3           7.3           2.0        1.0   \n",
       "1                    0.3           7.3           2.0        1.0   \n",
       "\n",
       "   congestion_surcharge  \n",
       "0                   0.0  \n",
       "1                   0.0  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%time\n",
    "df=dd_csv\n",
    "df.head(2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "4b31bc70",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
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
       "      <th>VendorID</th>\n",
       "      <th>RatecodeID</th>\n",
       "      <th>PULocationID</th>\n",
       "      <th>DOLocationID</th>\n",
       "      <th>passenger_count</th>\n",
       "      <th>trip_distance</th>\n",
       "      <th>fare_amount</th>\n",
       "      <th>extra</th>\n",
       "      <th>mta_tax</th>\n",
       "      <th>tip_amount</th>\n",
       "      <th>tolls_amount</th>\n",
       "      <th>improvement_surcharge</th>\n",
       "      <th>total_amount</th>\n",
       "      <th>payment_type</th>\n",
       "      <th>trip_type</th>\n",
       "      <th>congestion_surcharge</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74</td>\n",
       "      <td>75</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.47</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.3</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74</td>\n",
       "      <td>75</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.49</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.3</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   VendorID  RatecodeID  PULocationID  DOLocationID  passenger_count  \\\n",
       "0       2.0         1.0            74            75              1.0   \n",
       "1       2.0         1.0            74            75              1.0   \n",
       "\n",
       "   trip_distance  fare_amount  extra  mta_tax  tip_amount  tolls_amount  \\\n",
       "0           1.47          6.5    0.0      0.5         0.0             0   \n",
       "1           1.49          6.5    0.0      0.5         0.0             0   \n",
       "\n",
       "   improvement_surcharge  total_amount  payment_type  trip_type  \\\n",
       "0                    0.3           7.3           2.0        1.0   \n",
       "1                    0.3           7.3           2.0        1.0   \n",
       "\n",
       "   congestion_surcharge  \n",
       "0                   0.0  \n",
       "1                   0.0  "
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%time\n",
    "df1 = data\n",
    "df1.head(2)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1e47eff2",
   "metadata": {},
   "source": [
    "## EDA"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "83cb3cdd",
   "metadata": {},
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
       "      <th>VendorID</th>\n",
       "      <th>RatecodeID</th>\n",
       "      <th>PULocationID</th>\n",
       "      <th>DOLocationID</th>\n",
       "      <th>passenger_count</th>\n",
       "      <th>trip_distance</th>\n",
       "      <th>fare_amount</th>\n",
       "      <th>extra</th>\n",
       "      <th>mta_tax</th>\n",
       "      <th>tip_amount</th>\n",
       "      <th>tolls_amount</th>\n",
       "      <th>improvement_surcharge</th>\n",
       "      <th>total_amount</th>\n",
       "      <th>payment_type</th>\n",
       "      <th>trip_type</th>\n",
       "      <th>congestion_surcharge</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.47</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.30</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.49</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.30</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.31</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.30</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.43</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.30</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>74.0</td>\n",
       "      <td>75.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.10</td>\n",
       "      <td>6.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>7.30</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048570</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>166.0</td>\n",
       "      <td>181.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>10.51</td>\n",
       "      <td>40.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>8.81</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>52.86</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048571</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>166.0</td>\n",
       "      <td>186.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>5.07</td>\n",
       "      <td>19.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>4.61</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>27.66</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048572</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>166.0</td>\n",
       "      <td>79.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>7.32</td>\n",
       "      <td>24.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>2.50</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>31.05</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048573</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>166.0</td>\n",
       "      <td>141.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3.72</td>\n",
       "      <td>13.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>3.51</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>21.06</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048574</th>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>166.0</td>\n",
       "      <td>237.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3.68</td>\n",
       "      <td>15.0</td>\n",
       "      <td>0.5</td>\n",
       "      <td>0.5</td>\n",
       "      <td>3.81</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.3</td>\n",
       "      <td>22.86</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>1048575 rows × 16 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "         VendorID  RatecodeID  PULocationID  DOLocationID  passenger_count  \\\n",
       "0             2.0         1.0          74.0          75.0              1.0   \n",
       "1             2.0         1.0          74.0          75.0              1.0   \n",
       "2             2.0         1.0          74.0          75.0              1.0   \n",
       "3             2.0         1.0          74.0          75.0              1.0   \n",
       "4             2.0         1.0          74.0          75.0              1.0   \n",
       "...           ...         ...           ...           ...              ...   \n",
       "1048570       2.0         1.0         166.0         181.0              1.0   \n",
       "1048571       2.0         1.0         166.0         186.0              1.0   \n",
       "1048572       2.0         1.0         166.0          79.0              1.0   \n",
       "1048573       2.0         1.0         166.0         141.0              1.0   \n",
       "1048574       2.0         1.0         166.0         237.0              1.0   \n",
       "\n",
       "         trip_distance  fare_amount  extra  mta_tax  tip_amount  tolls_amount  \\\n",
       "0                 1.47          6.5    0.0      0.5        0.00           0.0   \n",
       "1                 1.49          6.5    0.0      0.5        0.00           0.0   \n",
       "2                 1.31          6.5    0.0      0.5        0.00           0.0   \n",
       "3                 1.43          6.5    0.0      0.5        0.00           0.0   \n",
       "4                 1.10          6.5    0.0      0.5        0.00           0.0   \n",
       "...                ...          ...    ...      ...         ...           ...   \n",
       "1048570          10.51         40.0    0.5      0.5        8.81           0.0   \n",
       "1048571           5.07         19.0    0.5      0.5        4.61           0.0   \n",
       "1048572           7.32         24.5    0.5      0.5        2.50           0.0   \n",
       "1048573           3.72         13.5    0.5      0.5        3.51           0.0   \n",
       "1048574           3.68         15.0    0.5      0.5        3.81           0.0   \n",
       "\n",
       "         improvement_surcharge  total_amount  payment_type  trip_type  \\\n",
       "0                          0.3          7.30           2.0        1.0   \n",
       "1                          0.3          7.30           2.0        1.0   \n",
       "2                          0.3          7.30           2.0        1.0   \n",
       "3                          0.3          7.30           2.0        1.0   \n",
       "4                          0.3          7.30           2.0        1.0   \n",
       "...                        ...           ...           ...        ...   \n",
       "1048570                    0.3         52.86           1.0        1.0   \n",
       "1048571                    0.3         27.66           1.0        1.0   \n",
       "1048572                    0.3         31.05           1.0        1.0   \n",
       "1048573                    0.3         21.06           1.0        1.0   \n",
       "1048574                    0.3         22.86           1.0        1.0   \n",
       "\n",
       "         congestion_surcharge  \n",
       "0                        0.00  \n",
       "1                        0.00  \n",
       "2                        0.00  \n",
       "3                        0.00  \n",
       "4                        0.00  \n",
       "...                       ...  \n",
       "1048570                  2.75  \n",
       "1048571                  2.75  \n",
       "1048572                  2.75  \n",
       "1048573                  2.75  \n",
       "1048574                  2.75  \n",
       "\n",
       "[1048575 rows x 16 columns]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Dask dataframe\n",
    "df.compute()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "d9a95d03",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(1048575, 16)"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Pandas Dataframe\n",
    "df1.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3c4be1e1",
   "metadata": {},
   "source": [
    "#### There are total 1048575 rows and 16 columns in both Datasets"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "a348d521",
   "metadata": {},
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
       "      <th>VendorID</th>\n",
       "      <th>RatecodeID</th>\n",
       "      <th>PULocationID</th>\n",
       "      <th>DOLocationID</th>\n",
       "      <th>passenger_count</th>\n",
       "      <th>trip_distance</th>\n",
       "      <th>fare_amount</th>\n",
       "      <th>extra</th>\n",
       "      <th>mta_tax</th>\n",
       "      <th>tip_amount</th>\n",
       "      <th>tolls_amount</th>\n",
       "      <th>improvement_surcharge</th>\n",
       "      <th>total_amount</th>\n",
       "      <th>payment_type</th>\n",
       "      <th>trip_type</th>\n",
       "      <th>congestion_surcharge</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>815482.000000</td>\n",
       "      <td>815482.000000</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>815482.000000</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1048575.0</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>815482.000000</td>\n",
       "      <td>815478.000000</td>\n",
       "      <td>815482.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1.799116</td>\n",
       "      <td>1.121824</td>\n",
       "      <td>1.058664e+02</td>\n",
       "      <td>1.262041e+02</td>\n",
       "      <td>1.321799</td>\n",
       "      <td>5.232639e+00</td>\n",
       "      <td>1.442554e+01</td>\n",
       "      <td>7.763946e-01</td>\n",
       "      <td>3.904208e-01</td>\n",
       "      <td>4.367562e-01</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.899481e-01</td>\n",
       "      <td>1.658424e+01</td>\n",
       "      <td>1.671317</td>\n",
       "      <td>1.027952</td>\n",
       "      <td>0.419597</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>0.400661</td>\n",
       "      <td>0.737862</td>\n",
       "      <td>6.979947e+01</td>\n",
       "      <td>7.623252e+01</td>\n",
       "      <td>0.993347</td>\n",
       "      <td>4.416213e+02</td>\n",
       "      <td>1.164878e+01</td>\n",
       "      <td>1.060924e+00</td>\n",
       "      <td>2.115034e-01</td>\n",
       "      <td>1.634329e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>6.017557e-02</td>\n",
       "      <td>1.223139e+01</td>\n",
       "      <td>0.505624</td>\n",
       "      <td>0.164835</td>\n",
       "      <td>0.988741</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>-2.425000e+01</td>\n",
       "      <td>-2.100000e+02</td>\n",
       "      <td>-4.500000e+00</td>\n",
       "      <td>-5.000000e-01</td>\n",
       "      <td>-3.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-3.000000e-01</td>\n",
       "      <td>-2.103000e+02</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>-2.750000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>4.900000e+01</td>\n",
       "      <td>6.100000e+01</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>7.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>8.300000e+00</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>7.600000e+01</td>\n",
       "      <td>1.190000e+02</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.900000e+00</td>\n",
       "      <td>1.100000e+01</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>1.280000e+01</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.590000e+02</td>\n",
       "      <td>1.890000e+02</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>3.860000e+00</td>\n",
       "      <td>1.900000e+01</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>2.174000e+01</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>99.000000</td>\n",
       "      <td>2.650000e+02</td>\n",
       "      <td>2.650000e+02</td>\n",
       "      <td>9.000000</td>\n",
       "      <td>1.599072e+05</td>\n",
       "      <td>8.030000e+02</td>\n",
       "      <td>1.426000e+01</td>\n",
       "      <td>3.550000e+00</td>\n",
       "      <td>6.412000e+02</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>8.038000e+02</td>\n",
       "      <td>5.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>2.750000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "            VendorID     RatecodeID  PULocationID  DOLocationID  \\\n",
       "count  815482.000000  815482.000000  1.048575e+06  1.048575e+06   \n",
       "mean        1.799116       1.121824  1.058664e+02  1.262041e+02   \n",
       "std         0.400661       0.737862  6.979947e+01  7.623252e+01   \n",
       "min         1.000000       1.000000  1.000000e+00  1.000000e+00   \n",
       "25%         2.000000       1.000000  4.900000e+01  6.100000e+01   \n",
       "50%         2.000000       1.000000  7.600000e+01  1.190000e+02   \n",
       "75%         2.000000       1.000000  1.590000e+02  1.890000e+02   \n",
       "max         2.000000      99.000000  2.650000e+02  2.650000e+02   \n",
       "\n",
       "       passenger_count  trip_distance   fare_amount         extra  \\\n",
       "count    815482.000000   1.048575e+06  1.048575e+06  1.048575e+06   \n",
       "mean          1.321799   5.232639e+00  1.442554e+01  7.763946e-01   \n",
       "std           0.993347   4.416213e+02  1.164878e+01  1.060924e+00   \n",
       "min           0.000000  -2.425000e+01 -2.100000e+02 -4.500000e+00   \n",
       "25%           1.000000   1.000000e+00  7.000000e+00  0.000000e+00   \n",
       "50%           1.000000   1.900000e+00  1.100000e+01  5.000000e-01   \n",
       "75%           1.000000   3.860000e+00  1.900000e+01  1.000000e+00   \n",
       "max           9.000000   1.599072e+05  8.030000e+02  1.426000e+01   \n",
       "\n",
       "            mta_tax    tip_amount  tolls_amount  improvement_surcharge  \\\n",
       "count  1.048575e+06  1.048575e+06     1048575.0           1.048575e+06   \n",
       "mean   3.904208e-01  4.367562e-01           0.0           2.899481e-01   \n",
       "std    2.115034e-01  1.634329e+00           0.0           6.017557e-02   \n",
       "min   -5.000000e-01 -3.000000e+00           0.0          -3.000000e-01   \n",
       "25%    5.000000e-01  0.000000e+00           0.0           3.000000e-01   \n",
       "50%    5.000000e-01  0.000000e+00           0.0           3.000000e-01   \n",
       "75%    5.000000e-01  0.000000e+00           0.0           3.000000e-01   \n",
       "max    3.550000e+00  6.412000e+02           0.0           3.000000e-01   \n",
       "\n",
       "       total_amount   payment_type      trip_type  congestion_surcharge  \n",
       "count  1.048575e+06  815482.000000  815478.000000         815482.000000  \n",
       "mean   1.658424e+01       1.671317       1.027952              0.419597  \n",
       "std    1.223139e+01       0.505624       0.164835              0.988741  \n",
       "min   -2.103000e+02       1.000000       1.000000             -2.750000  \n",
       "25%    8.300000e+00       1.000000       1.000000              0.000000  \n",
       "50%    1.280000e+01       2.000000       1.000000              0.000000  \n",
       "75%    2.174000e+01       2.000000       1.000000              0.000000  \n",
       "max    8.038000e+02       5.000000       2.000000              2.750000  "
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe().compute()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "43ec6db5",
   "metadata": {},
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
       "      <th>VendorID</th>\n",
       "      <th>RatecodeID</th>\n",
       "      <th>PULocationID</th>\n",
       "      <th>DOLocationID</th>\n",
       "      <th>passenger_count</th>\n",
       "      <th>trip_distance</th>\n",
       "      <th>fare_amount</th>\n",
       "      <th>extra</th>\n",
       "      <th>mta_tax</th>\n",
       "      <th>tip_amount</th>\n",
       "      <th>tolls_amount</th>\n",
       "      <th>improvement_surcharge</th>\n",
       "      <th>total_amount</th>\n",
       "      <th>payment_type</th>\n",
       "      <th>trip_type</th>\n",
       "      <th>congestion_surcharge</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>815482.000000</td>\n",
       "      <td>815482.000000</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>815482.000000</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1048575.0</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>1.048575e+06</td>\n",
       "      <td>815482.000000</td>\n",
       "      <td>815478.000000</td>\n",
       "      <td>815482.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1.799116</td>\n",
       "      <td>1.121824</td>\n",
       "      <td>1.058664e+02</td>\n",
       "      <td>1.262041e+02</td>\n",
       "      <td>1.321799</td>\n",
       "      <td>5.232639e+00</td>\n",
       "      <td>1.442554e+01</td>\n",
       "      <td>7.763946e-01</td>\n",
       "      <td>3.904208e-01</td>\n",
       "      <td>4.367562e-01</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.899481e-01</td>\n",
       "      <td>1.658424e+01</td>\n",
       "      <td>1.671317</td>\n",
       "      <td>1.027952</td>\n",
       "      <td>0.419597</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>0.400661</td>\n",
       "      <td>0.737862</td>\n",
       "      <td>6.979947e+01</td>\n",
       "      <td>7.623252e+01</td>\n",
       "      <td>0.993347</td>\n",
       "      <td>4.416213e+02</td>\n",
       "      <td>1.164878e+01</td>\n",
       "      <td>1.060924e+00</td>\n",
       "      <td>2.115034e-01</td>\n",
       "      <td>1.634329e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>6.017557e-02</td>\n",
       "      <td>1.223139e+01</td>\n",
       "      <td>0.505624</td>\n",
       "      <td>0.164835</td>\n",
       "      <td>0.988741</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>-2.425000e+01</td>\n",
       "      <td>-2.100000e+02</td>\n",
       "      <td>-4.500000e+00</td>\n",
       "      <td>-5.000000e-01</td>\n",
       "      <td>-3.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-3.000000e-01</td>\n",
       "      <td>-2.103000e+02</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>-2.750000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>4.900000e+01</td>\n",
       "      <td>6.100000e+01</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>7.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>8.300000e+00</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>7.600000e+01</td>\n",
       "      <td>1.190000e+02</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.900000e+00</td>\n",
       "      <td>1.100000e+01</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>1.280000e+01</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.590000e+02</td>\n",
       "      <td>1.890000e+02</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>3.860000e+00</td>\n",
       "      <td>1.900000e+01</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>5.000000e-01</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>2.174000e+01</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>99.000000</td>\n",
       "      <td>2.650000e+02</td>\n",
       "      <td>2.650000e+02</td>\n",
       "      <td>9.000000</td>\n",
       "      <td>1.599072e+05</td>\n",
       "      <td>8.030000e+02</td>\n",
       "      <td>1.426000e+01</td>\n",
       "      <td>3.550000e+00</td>\n",
       "      <td>6.412000e+02</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.000000e-01</td>\n",
       "      <td>8.038000e+02</td>\n",
       "      <td>5.000000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>2.750000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "            VendorID     RatecodeID  PULocationID  DOLocationID  \\\n",
       "count  815482.000000  815482.000000  1.048575e+06  1.048575e+06   \n",
       "mean        1.799116       1.121824  1.058664e+02  1.262041e+02   \n",
       "std         0.400661       0.737862  6.979947e+01  7.623252e+01   \n",
       "min         1.000000       1.000000  1.000000e+00  1.000000e+00   \n",
       "25%         2.000000       1.000000  4.900000e+01  6.100000e+01   \n",
       "50%         2.000000       1.000000  7.600000e+01  1.190000e+02   \n",
       "75%         2.000000       1.000000  1.590000e+02  1.890000e+02   \n",
       "max         2.000000      99.000000  2.650000e+02  2.650000e+02   \n",
       "\n",
       "       passenger_count  trip_distance   fare_amount         extra  \\\n",
       "count    815482.000000   1.048575e+06  1.048575e+06  1.048575e+06   \n",
       "mean          1.321799   5.232639e+00  1.442554e+01  7.763946e-01   \n",
       "std           0.993347   4.416213e+02  1.164878e+01  1.060924e+00   \n",
       "min           0.000000  -2.425000e+01 -2.100000e+02 -4.500000e+00   \n",
       "25%           1.000000   1.000000e+00  7.000000e+00  0.000000e+00   \n",
       "50%           1.000000   1.900000e+00  1.100000e+01  5.000000e-01   \n",
       "75%           1.000000   3.860000e+00  1.900000e+01  1.000000e+00   \n",
       "max           9.000000   1.599072e+05  8.030000e+02  1.426000e+01   \n",
       "\n",
       "            mta_tax    tip_amount  tolls_amount  improvement_surcharge  \\\n",
       "count  1.048575e+06  1.048575e+06     1048575.0           1.048575e+06   \n",
       "mean   3.904208e-01  4.367562e-01           0.0           2.899481e-01   \n",
       "std    2.115034e-01  1.634329e+00           0.0           6.017557e-02   \n",
       "min   -5.000000e-01 -3.000000e+00           0.0          -3.000000e-01   \n",
       "25%    5.000000e-01  0.000000e+00           0.0           3.000000e-01   \n",
       "50%    5.000000e-01  0.000000e+00           0.0           3.000000e-01   \n",
       "75%    5.000000e-01  0.000000e+00           0.0           3.000000e-01   \n",
       "max    3.550000e+00  6.412000e+02           0.0           3.000000e-01   \n",
       "\n",
       "       total_amount   payment_type      trip_type  congestion_surcharge  \n",
       "count  1.048575e+06  815482.000000  815478.000000         815482.000000  \n",
       "mean   1.658424e+01       1.671317       1.027952              0.419597  \n",
       "std    1.223139e+01       0.505624       0.164835              0.988741  \n",
       "min   -2.103000e+02       1.000000       1.000000             -2.750000  \n",
       "25%    8.300000e+00       1.000000       1.000000              0.000000  \n",
       "50%    1.280000e+01       2.000000       1.000000              0.000000  \n",
       "75%    2.174000e+01       2.000000       1.000000              0.000000  \n",
       "max    8.038000e+02       5.000000       2.000000              2.750000  "
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "49cac5db",
   "metadata": {},
   "source": [
    "#### Both data sets have means at 2.00 and std at 0.400661"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1dc6450f",
   "metadata": {},
   "source": [
    "##### Removing missing data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "8d95d6f2",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "VendorID                 233093\n",
       "RatecodeID               233093\n",
       "PULocationID                  0\n",
       "DOLocationID                  0\n",
       "passenger_count          233093\n",
       "trip_distance                 0\n",
       "fare_amount                   0\n",
       "extra                         0\n",
       "mta_tax                       0\n",
       "tip_amount                    0\n",
       "tolls_amount                  0\n",
       "improvement_surcharge         0\n",
       "total_amount                  0\n",
       "payment_type             233093\n",
       "trip_type                233097\n",
       "congestion_surcharge     233093\n",
       "dtype: int64"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%time\n",
    "df1.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "e264d3ff",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "VendorID                 233093\n",
       "RatecodeID               233093\n",
       "PULocationID                  0\n",
       "DOLocationID                  0\n",
       "passenger_count          233093\n",
       "trip_distance                 0\n",
       "fare_amount                   0\n",
       "extra                         0\n",
       "mta_tax                       0\n",
       "tip_amount                    0\n",
       "tolls_amount                  0\n",
       "improvement_surcharge         0\n",
       "total_amount                  0\n",
       "payment_type             233093\n",
       "trip_type                233097\n",
       "congestion_surcharge     233093\n",
       "dtype: int64"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%time\n",
    "df.isnull().compute().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "a45ddb2a",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "VendorID                 0\n",
       "RatecodeID               0\n",
       "PULocationID             0\n",
       "DOLocationID             0\n",
       "passenger_count          0\n",
       "trip_distance            0\n",
       "fare_amount              0\n",
       "extra                    0\n",
       "mta_tax                  0\n",
       "tip_amount               0\n",
       "tolls_amount             0\n",
       "improvement_surcharge    0\n",
       "total_amount             0\n",
       "payment_type             0\n",
       "trip_type                0\n",
       "congestion_surcharge     0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%time\n",
    "df1=df1.fillna(0)\n",
    "df1.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "ddc2649a",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "VendorID                 0\n",
       "RatecodeID               0\n",
       "PULocationID             0\n",
       "DOLocationID             0\n",
       "passenger_count          0\n",
       "trip_distance            0\n",
       "fare_amount              0\n",
       "extra                    0\n",
       "mta_tax                  0\n",
       "tip_amount               0\n",
       "tolls_amount             0\n",
       "improvement_surcharge    0\n",
       "total_amount             0\n",
       "payment_type             0\n",
       "trip_type                0\n",
       "congestion_surcharge     0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%time\n",
    "df=df.fillna(0)\n",
    "df.isnull().sum().compute()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5a436672",
   "metadata": {},
   "source": [
    "### Correlation "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "c552312b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 720x576 with 2 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize=(10, 8))\n",
    "sns.heatmap(data.drop('fare_amount', axis=1).corr(),cmap='coolwarm',vmin=0, vmax=1,square=True)\n",
    "plt.show();"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6f301df6",
   "metadata": {},
   "source": [
    "### Feature Scaling"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "99d026b0",
   "metadata": {},
   "outputs": [],
   "source": [
    "from dask_ml.preprocessing import RobustScaler"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "ac87d01e",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    }
   ],
   "source": [
    "#Feature scaling for DASK dataframe\n",
    "%time\n",
    "transformer = RobustScaler().fit(df)\n",
    "df=transformer.transform(df)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "3754d885",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.preprocessing import RobustScaler"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "02fab955",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    }
   ],
   "source": [
    "#Feature scaling pandas dataframe\n",
    "%time\n",
    "transformer1= RobustScaler().fit(df1)\n",
    "df1= transformer1.transform(df1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "8342471f",
   "metadata": {},
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
       "      <th>VendorID</th>\n",
       "      <th>RatecodeID</th>\n",
       "      <th>PULocationID</th>\n",
       "      <th>DOLocationID</th>\n",
       "      <th>passenger_count</th>\n",
       "      <th>trip_distance</th>\n",
       "      <th>fare_amount</th>\n",
       "      <th>extra</th>\n",
       "      <th>mta_tax</th>\n",
       "      <th>tip_amount</th>\n",
       "      <th>tolls_amount</th>\n",
       "      <th>improvement_surcharge</th>\n",
       "      <th>total_amount</th>\n",
       "      <th>payment_type</th>\n",
       "      <th>trip_type</th>\n",
       "      <th>congestion_surcharge</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.018182</td>\n",
       "      <td>-0.343750</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.150350</td>\n",
       "      <td>-0.375000</td>\n",
       "      <td>-0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.409226</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.018182</td>\n",
       "      <td>-0.343750</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.143357</td>\n",
       "      <td>-0.375000</td>\n",
       "      <td>-0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.409226</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.018182</td>\n",
       "      <td>-0.343750</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.206294</td>\n",
       "      <td>-0.375000</td>\n",
       "      <td>-0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.409226</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.018182</td>\n",
       "      <td>-0.343750</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.164336</td>\n",
       "      <td>-0.375000</td>\n",
       "      <td>-0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.409226</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.018182</td>\n",
       "      <td>-0.343750</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.279720</td>\n",
       "      <td>-0.375000</td>\n",
       "      <td>-0.5</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.409226</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048570</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.818182</td>\n",
       "      <td>0.484375</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.010490</td>\n",
       "      <td>2.416667</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>8.81</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.980655</td>\n",
       "      <td>-1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048571</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.818182</td>\n",
       "      <td>0.523438</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.108392</td>\n",
       "      <td>0.666667</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>4.61</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.105655</td>\n",
       "      <td>-1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048572</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.818182</td>\n",
       "      <td>-0.312500</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.895105</td>\n",
       "      <td>1.125000</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.50</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1.357887</td>\n",
       "      <td>-1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048573</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.818182</td>\n",
       "      <td>0.171875</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.636364</td>\n",
       "      <td>0.208333</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.51</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.614583</td>\n",
       "      <td>-1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1048574</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.818182</td>\n",
       "      <td>0.921875</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.622378</td>\n",
       "      <td>0.333333</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>3.81</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.748512</td>\n",
       "      <td>-1.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>2.75</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>1048575 rows × 16 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "         VendorID  RatecodeID  PULocationID  DOLocationID  passenger_count  \\\n",
       "0             0.0         0.0     -0.018182     -0.343750              0.0   \n",
       "1             0.0         0.0     -0.018182     -0.343750              0.0   \n",
       "2             0.0         0.0     -0.018182     -0.343750              0.0   \n",
       "3             0.0         0.0     -0.018182     -0.343750              0.0   \n",
       "4             0.0         0.0     -0.018182     -0.343750              0.0   \n",
       "...           ...         ...           ...           ...              ...   \n",
       "1048570       0.0         0.0      0.818182      0.484375              0.0   \n",
       "1048571       0.0         0.0      0.818182      0.523438              0.0   \n",
       "1048572       0.0         0.0      0.818182     -0.312500              0.0   \n",
       "1048573       0.0         0.0      0.818182      0.171875              0.0   \n",
       "1048574       0.0         0.0      0.818182      0.921875              0.0   \n",
       "\n",
       "         trip_distance  fare_amount  extra  mta_tax  tip_amount  tolls_amount  \\\n",
       "0            -0.150350    -0.375000   -0.5      0.0        0.00           0.0   \n",
       "1            -0.143357    -0.375000   -0.5      0.0        0.00           0.0   \n",
       "2            -0.206294    -0.375000   -0.5      0.0        0.00           0.0   \n",
       "3            -0.164336    -0.375000   -0.5      0.0        0.00           0.0   \n",
       "4            -0.279720    -0.375000   -0.5      0.0        0.00           0.0   \n",
       "...                ...          ...    ...      ...         ...           ...   \n",
       "1048570       3.010490     2.416667    0.0      0.0        8.81           0.0   \n",
       "1048571       1.108392     0.666667    0.0      0.0        4.61           0.0   \n",
       "1048572       1.895105     1.125000    0.0      0.0        2.50           0.0   \n",
       "1048573       0.636364     0.208333    0.0      0.0        3.51           0.0   \n",
       "1048574       0.622378     0.333333    0.0      0.0        3.81           0.0   \n",
       "\n",
       "         improvement_surcharge  total_amount  payment_type  trip_type  \\\n",
       "0                          0.0     -0.409226           0.0        0.0   \n",
       "1                          0.0     -0.409226           0.0        0.0   \n",
       "2                          0.0     -0.409226           0.0        0.0   \n",
       "3                          0.0     -0.409226           0.0        0.0   \n",
       "4                          0.0     -0.409226           0.0        0.0   \n",
       "...                        ...           ...           ...        ...   \n",
       "1048570                    0.0      2.980655          -1.0        0.0   \n",
       "1048571                    0.0      1.105655          -1.0        0.0   \n",
       "1048572                    0.0      1.357887          -1.0        0.0   \n",
       "1048573                    0.0      0.614583          -1.0        0.0   \n",
       "1048574                    0.0      0.748512          -1.0        0.0   \n",
       "\n",
       "         congestion_surcharge  \n",
       "0                        0.00  \n",
       "1                        0.00  \n",
       "2                        0.00  \n",
       "3                        0.00  \n",
       "4                        0.00  \n",
       "...                       ...  \n",
       "1048570                  2.75  \n",
       "1048571                  2.75  \n",
       "1048572                  2.75  \n",
       "1048573                  2.75  \n",
       "1048574                  2.75  \n",
       "\n",
       "[1048575 rows x 16 columns]"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Convert numpy array after feature scaling to pandas dataframe\n",
    "df2= pd.DataFrame(df1, columns = ['VendorID','RatecodeID','PULocationID','DOLocationID','passenger_count','trip_distance','fare_amount','extra','mta_tax','tip_amount','tolls_amount','improvement_surcharge','total_amount','payment_type','trip_type','congestion_surcharge'])\n",
    "df2"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5b950aa2",
   "metadata": {},
   "source": [
    "## Machine Learning"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "07c043b6",
   "metadata": {},
   "source": [
    "#### Dependent and independent variables"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "ff56c3dc",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Dask Dataframe dependent and independent variables\n",
    "X= df.drop(['VendorID','RatecodeID'],axis=1)\n",
    "y= df[('total_amount')]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "b6753486",
   "metadata": {},
   "outputs": [],
   "source": [
    "# pandas Dataframe dependent and independent variables\n",
    "X1 = df2.drop(['VendorID','RatecodeID'], axis=1)\n",
    "Y1 = df2['total_amount']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "632d23e0",
   "metadata": {},
   "outputs": [],
   "source": [
    "from dask_ml.model_selection import train_test_split"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "95a4846f",
   "metadata": {},
   "source": [
    "#### Split the data into training and testing set and set the random state to 100"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "f5c9fe42",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n",
      "(Delayed('int-06b236a2-707a-4a2d-8f23-6ccedaa608bc'), 14) (dd.Scalar<size-ag..., dtype=int32>,)\n",
      "(Delayed('int-f97b0602-7e6f-4b98-918b-84bde1c9e866'), 14) (dd.Scalar<size-ag..., dtype=int32>,)\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Anaconda\\lib\\site-packages\\dask_ml\\model_selection\\_split.py:462: FutureWarning: The default value for 'shuffle' must be specified when splitting DataFrames. In the future DataFrames will automatically be shuffled within blocks prior to splitting. Specify 'shuffle=True' to adopt the future behavior now, or 'shuffle=False' to retain the previous behavior.\n",
      "  warnings.warn(\n"
     ]
    }
   ],
   "source": [
    "# Dask data split intro training and testing sets\n",
    "%time\n",
    "xtrain, xtest, ytrain, ytest = train_test_split(X, y,train_size=0.7,  test_size=0.3,random_state=100)\n",
    "print(xtrain.shape, ytrain.shape)\n",
    "print(xtest.shape, ytest.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "949cf609",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "79909e64",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n",
      "(734002, 14) (734002,)\n",
      "(314573, 14) (314573,)\n"
     ]
    }
   ],
   "source": [
    "# Pandas data split intro training and testing data sets\n",
    "%time\n",
    "xtrain1, xtest1, ytrain1, ytest1 = train_test_split(X1, Y1, test_size=0.3,random_state=100)\n",
    "print(xtrain1.shape, ytrain1.shape)\n",
    "print(xtest1.shape, ytest1.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "3beceb49",
   "metadata": {},
   "outputs": [],
   "source": [
    "import xgboost\n",
    "import dask_xgboost"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d4a375b3",
   "metadata": {},
   "source": [
    "### Training time using DASK dataframe dd vs. Pandas dataframe pd "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "34f5211c",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "----------------------------------\n",
      " | Dask training time:  76.51860690116882 seconds |\n",
      "----------------------------------\n"
     ]
    }
   ],
   "source": [
    "start_time = time.time()\n",
    "\n",
    "params = {'objective':'reg:squarederror','nround': 1000, \n",
    "          'max_depth': 16, 'eta': 0.01, 'subsample': 0.5, \n",
    "          'min_child_weight': 1}\n",
    "bst = dask_xgboost.train(client, params, xtrain, ytrain, num_boost_round=100)\n",
    "bst\n",
    "print(\"----------------------------------\")\n",
    "print(\" | Dask training time:  %s seconds |\" % (time.time() - start_time))\n",
    "print(\"----------------------------------\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "cd3b4707",
   "metadata": {},
   "outputs": [],
   "source": [
    "import xgboost as xgb"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "id": "3049d4c3",
   "metadata": {},
   "outputs": [],
   "source": [
    "params1 = {'objective':'reg:squarederror','n_estimators':1000, \n",
    "          'max_depth': 16, 'eta': 0.01, 'subsample': 0.5, \n",
    "          'min_child_weight': 1}\n",
    "reg_xgb = xgb.XGBRegressor(**params1,seed=25,nthread=1,random_state=100)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "id": "edd5e848",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "----------------------------------\n",
      " | Pandas training time:  1279.772429227829 seconds |\n",
      "----------------------------------\n"
     ]
    }
   ],
   "source": [
    "start_time = time.time()\n",
    "reg_xgb.fit(xtrain1, ytrain1)\n",
    "print(\"----------------------------------\")\n",
    "print(\" | Pandas training time:  %s seconds |\" % (time.time() - start_time))\n",
    "print(\"----------------------------------\")"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "203e4ad3",
   "metadata": {},
   "source": [
    "## Prediction"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "40e1a193",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "array([-0.07581281, -0.07581281, -0.07581281, ...,  0.8778246 ,\n",
       "        1.9313626 ,  0.6678274 ], dtype=float32)"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Dask Dataframe prediction\n",
    "%time\n",
    "y_hat = dask_xgboost.predict(client, bst, xtest).persist()\n",
    "y_hat.compute()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "id": "a3c3ad83",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "array([ 0.27902764, -0.29758498, -0.5207888 , ..., -0.2603835 ,\n",
       "        1.0602419 ,  0.11162405], dtype=float32)"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Pandas Dataframe prediction\n",
    "%time\n",
    "xgb_pred = reg_xgb.predict(xtest1)\n",
    "xgb_pred"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "404f791b",
   "metadata": {},
   "source": [
    "#### Feature importance "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "id": "7426be15",
   "metadata": {},
   "outputs": [],
   "source": [
    "%matplotlib inline\n",
    "import matplotlib.pyplot as plt"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "id": "1a8d2dd9",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "#Dask\n",
    "%time\n",
    "ax = xgboost.plot_importance(bst, height=0.8, max_num_features=9)\n",
    "ax.grid(False, axis=\"y\")\n",
    "ax.set_title('Estimated feature importance')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "id": "59b29b13",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Wall time: 0 ns\n"
     ]
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "#Pandas\n",
    "%time\n",
    "bx = xgboost.plot_importance(reg_xgb, height=0.8, max_num_features=9)\n",
    "bx.grid(False, axis=\"y\")\n",
    "bx.set_title('Estimated feature importance')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "469246cb",
   "metadata": {},
   "source": [
    "#### Result: Machine learning using Dask data frame is significantly faster than Pandas data frame because of parallel computing. Dask can be very useful when working with large datasets for machine learning as compared to Pandas dataframe which take significant amount of time. We can see the training times of both Dask and Pandas in this notebook.   "
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
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
   "version": "3.9.12"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
