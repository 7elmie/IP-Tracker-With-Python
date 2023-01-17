# IP-Tracker-With-Python

This is Tool or source code Create to learn and level up technology knowledge 
i'm not responsible about bad use or any thing else this tool or code open source and Can use or edit or modify 

# First , let’s download some libraries than import them. Open your terminal and write these :

    pip install geocoder
    pip install folium
    
# Now let’s import these libraries. If you want some nice-looking title you can also use pyfiglet library.

    import geocoder # to locate the ip 
    import folium # to create a visual map 
    import codecs
    import optparse 3 to get input from terminal
    import time
    
    
# Now let’s create a function to get user input from terminal:

    import geocoder # to locate the ip 
    import folium # to create a visual map 
    import codecs
    import optparse # to get input from terminal
    import time
    def getting_input():
        object_parse = optparse.OptionParser() #creating optparse object
        object_parse.add_option("-i", "--ip", dest="ip", help="ip to change,if you want to search your ip, just type `me`") # creating the input
        return object_parse.parse_args()
    [user_input,arguements] = getting_input()  
    
    


# Now let’s find the location of the ip address chosen by the user:

    try:

        g = geocoder.ip(user_input.ip) #==> gets your ip address or put an ip address 

        myaddress = g.latlng # getting the cords
        time.sleep(1)

        print(myaddress) # printing the address
        my_map1 = folium.Map(location=myaddress,zoom_start=12) #creating the map 
        folium.CircleMarker(location=myaddress,radius=50,popup="Yorkshire").add_to(my_map1) # adding a circle to the the selected cords

        folium.Marker(location=myaddress,popup="Yorkshire").add_to(my_map1) #adding a marker to the selected cords

        my_map1.save("my_map.html")
    except:
        print("can not find the location of your IP!!!") #if ip is wrong print this:

