#/usr/bin/R

# Goal:  This script will help you clean up a data frame of user locations. As
#       an example, you may want to build a map of users tweeting about a 
#       particular subject. You must geocode their profile locations. But
#       some profile locations are intentionally vague ("Earth") or could
#       lead to incorrect guesses by geocoding software (is "Warzone Cashmere
#       Asia" a store or a reference to Kashmir?). The code here will help
#       you remove bad location info. Check any results you get, as this
#       code is likely not exhaustive.

# Contains:
#       1) A list of bad geocoding locations that I've found in Twitter user profiles
#          and code to remove them.
#       2) Code that does a reality check after you have geocoded. I've found
#          that Google often gives my country as the geocoded
#          location, when it is unable to find a proper location.

# Needs
library(dplyr)

# List of non-geocodable locations 
obscure_locations <- c("Warzone Cashmere Asia", "Roma", "All around the world"
        ,"iPhone", "lost", "PH", "Earth", "Hail", "Where I Am", "Shop the best for less"
        ,"mx", "The Web", "Internet", "Worldwide", "Home", "world", "World", "global"
        ,"Global", "Aa - Ad", "92", "youtube!!!!", "Where the beer is."
        ,"herts", "nowhere", "in transit", "Everywhere"
        ,"15 minutes of fame", "Above all", "On the moon", "moon")

# For a tibble of user info, where profile location info is $Location
User_Data <- User_Data %>%
        filter(!(Location %in% obscure_locations))

# After geocoding, this may be useful
# First, find locations that explicitly mention only your country, then invert the logical
# Make another logical for the formatted geocoding address being == your country
# Construct a compound logical to excise bad geocoding
not_USA <- !grepl("United|US|USA|America|U.S.|U.S.A.|United States of America|UNITED STATES OF AMERICA"
                    ,User_Data$Location)
geocode_USA <- User_Data$formatted_address == "United States"
Compound <- !(not_USA & geocode_USA)

User_Data <- User_Data %>%
        filter(Compound)
