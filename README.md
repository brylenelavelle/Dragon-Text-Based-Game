# Dragon-Text-Based-Game
rooms = {
        'Nidavellir': {'West': 'Tesseract', 'Item': 'Gauntlet'},
        'Tesseract': {'South': 'Xandar', 'West': 'Nidavellir', 'Item': 'Space Stone'},
        'Xandar': {'West': "Loki's Scepter", 'East': "Eye of Agomoto", 'South': "Planet Vormir", 'Item': 'Power Stone'},
        "Loki's Scepter": {'East': 'Xandar', 'Item': 'Mind Stone'},
        'Planet Vormir': {'East': 'Planet Titan', 'North': 'Xandar', 'Item': 'Soul Stone'},
        'Planet Titan': {'West': 'Planet Vormir', 'Item': 'Thanos'},
        'Eye of Agomoto': {'West': 'Xandar', 'North': 'Aether', 'Item': 'Time Stone'},
        'Aether': {'South': 'Eye of Agomoto', 'Item': 'Reality Stone'}
    }

current_room = 'Nidavellir'

def get_new_room(current_room, direction):
    new_room = current_room
    for i in rooms:
        if i == current_room:
            if direction in rooms[i]:
                new_room = rooms[i][direction]
    return new_room
def get_item(current_room):
    return rooms[current_room]['Item']

def instructions():
    print('Marvel Text Adventure Game')
    print('Collect 6 stones to win the game, or be terminated by Thanos.')
    print('Move commands: go North, go South, go East, go West')
    print("Add to Inventory: get 'item name'")
    print('Type "Exit" to exit the game.')
instructions()
inventory = []
while (1):
    print('You are in', current_room)
    print('Inventory:', inventory)
    item = get_item(current_room)
    print('You see a', item)
    if item == 'Thanos':
        print('Thanos has snapped his finger to terminate you! Game over!')
        exit(0)
    direction = input('Enter your move:')
    if (direction == 'go East' or direction == 'go West' or direction == 'go North' or direction == 'go South'):
        direction = direction[3:]
        new_room = get_new_room(current_room, direction)
        if new_room == current_room:
            print('You are about to run into a blackhole! Enter another direction!')
        else:
            current_room = new_room
    elif direction == 'Exit':
        exit(0)
    elif direction == str('get '+ item):
        if item in inventory:
            print('You already have that stone! Collect the others!')
        else:
            inventory.append(item)
    else:
        print('Invalid move!')
    if len(inventory) == 6:
        print('Congratulations! You have collected all stones and defeated Thanos!')
        exit(0)
