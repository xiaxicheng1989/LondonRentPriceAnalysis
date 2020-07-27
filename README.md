# London Rent Price Analysis
This project is part of the IBM data science professional certificate.  

The goal is to extract location data from platforms such as [Foursquare API](https://foursquare.com/) to solve real-life business problem. 

## 1. Business problem
To help smaller business owners in gastronomy expanding their business in London, exposure to the public is as important as a cheap and stable rent. Often, the individual stores are required to be self-supporting regarding groceries. Hence, they rely on the close-by supermarkets to avoid delivery costs. 

The outcome of the project is to provide a location recommendation services to these clients, which reveals the locations in London that are most suitable for the business owner.

## 2. Data
For now, I only use the following data to provide a location recommendation:  
- Rent prices statistics from London Datastore of MAYOR OF LONDON (<a href="https://data.london.gov.uk/dataset/average-private-rents-borough">data from 2011 to 2019</a>) 

- London borough's area sizes, population distribution and postal codes (<a href="https://www.doogal.co.uk/london_postcodes.php">data</a>)
- Sizes of London's boroughs are extracted from <a href="https://en.wikipedia.org/wiki/List_of_London_boroughs">Wikipedia</a> using webscrapping. The detailed postal codes across london are useful for more narrowed data collection using FourSquare.
    
- Venue data extraction using Foursquare after popularity (in particular, supermarkets/grocery shops)

### 2.1 Data cleansing
The rent price data and borough data are all fairly clean and don't require much processing. 

However, when collecting venue data using location data provider, I was limited by 100 venues per call on Foursquare, due to the free license. To maximise the number of outputs, I needed to use finer postal code of all london area, where each on average covers an area of 20m x 20m. After removing duplications, I ended up with over 300000 venues within over 300 categories across the entire city. The venue categories can be summarised by:

<img src="https://github.com/xiaxicheng1989/LondonRentPriceAnalysis/blob/master/Plots/CategoryDist.jpg" width="20%">

Out of these over 4000 are major supermarket chains, such as Tesco, Sainsbury's,... The figures below show the population density (left) and the supermarket density (right) by boroughs.

<img src="https://github.com/xiaxicheng1989/LondonRentPriceAnalysis/blob/master/Plots/LondonProperties.jpg" width="80%">
It is interesting to see that in the east and south London, the density of supermarket is low compared with the high population density, which could already indicate to potential areas to grow business.

## 3. Methodology
To quantify the rent price movement, the derived quantities about the rent prices: the mean rent price and annual rent increment in percentage are used for analysis. As part of the data exploration and to understand the available data, I use pairwise correlation and multilinear regression to analyse the rent dependence on the venue categories in each borough. The figure below shows the distribution for mean rent price (orange) and percentage annual rent increments (blue). 

<img src="https://github.com/xiaxicheng1989/LondonRentPriceAnalysis/blob/master/Plots/rentCorr.jpg" width="80%">
The mean rent price appears to be mainly driven by the number of restaurants, Hotels and grocery opportunities. Surprisingly, multi-dimensional linear regression suggests that the rent price is negative affected by the pub/bars and stores in the borough. On the other hand, the rental increments are only driven by the existing restaurants, in the absence of other categories of venues.

Extrapolation on the rent prices are made for the next 3, 5 and 10 years. These are compared with 
the population density, supermarket density to deliver a selection of boroughs. This selection is then separately confirmed by the technique: K-mean clustering.

## 4. Final recommendation
My analysis have shown that the most expensive borough is the Kensington and Chelsea, which is followed by Westminster. Boroughs located around these two appear to fall into the next rent price class. However, rent cost seems to be in general higher in the west than in the east. In contrast, east(north) and south(west) London appear to experience a larger annual rent increase. This trend indicates an higher demand in housing and show potential future development. Particular heavily developing boroughs are:
- Kingston, Hackney, Newham and Barking.

Using multi-dimensional linear regression, I found out that the mean rent price is mostly driven by the number of hotels, Grocery, Gym, Nature, which are all indications of balanced living options. Transport and supermarket don't really affect the rental price. Finally, I recommend:
– Camden, Hackney, Hammersmith and Fulham, Islington, Lambeth, Southwark, Tower Hamlets, Wandsworth and City of London
as suitable boroughs to expand the business, as illustrated in figure below in bright yellow:

<img src="https://github.com/xiaxicheng1989/LondonRentPriceAnalysis/blob/master/Plots/RecomKmena.jpg" width="80%">
