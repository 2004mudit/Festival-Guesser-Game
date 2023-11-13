import os

class FestivalNode:
    def __init__(self, query, festival=None):
        self.query = query
        self.festival = festival
        self.left = None
        self.right = None

class FestivalTree:
    def __init__(self):
        self.root = None

    def construct_tree(self, file_path):
        with open(file_path, 'r') as file:
            lines = file.readlines()
            self.root = self.construct_tree_recursive(lines)

    def construct_tree_recursive(self, lines):
        if not lines:
            return None

        line = lines.pop(0).strip()
        parts = line.split(" ", 1)
        address = int(parts[0])
        rest = parts[1]

        if rest.startswith("It's "):
            festival = rest.replace("It's ", "")
            return FestivalNode(None, festival)

        query = rest
        left_child = self.construct_tree_recursive(lines)
        right_child = self.construct_tree_recursive(lines)
        node = FestivalNode(query)
        node.left = left_child
        node.right = right_child

        return node

    def display_tree(self, node=None, indent="", last='updown', traversal='inorder'):
        if node is not None:
            if traversal == 'preorder':
                print(indent + (node.query if node.query else f"Festival: {node.festival}"))
            self.display_tree(node.left, indent, 'left', traversal)
            if traversal == 'inorder':
                print(indent + (node.query if node.query else f"Festival: {node.festival}"))
            self.display_tree(node.right, indent, 'right', traversal)
            if traversal == 'postorder':
                print(indent + (node.query if node.query else f"Festival: {node.festival}"))

    def play_festival_game(self, node=None):
        if node is None:
            node = self.root

        print("Please answer a series of questions, and I will tell you what Indian festival you are thinking about:")
        while node.left or node.right:
            answer = input(node.query).strip().upper()
            if answer == 'Y':
                node = node.left
            elif answer == 'N':
                node = node.right
            else:
                print("Please answer with 'Y' or 'N'.")
        print(f"It's '{node.festival}'.")

if __name__ == "__main__":
    festival_tree = FestivalTree()
    file_path = "festivals.txt"
    festival_tree.construct_tree(file_path)

    while True:
        print("…your festival choice: ")
        print("1. Play the festival game")
        print("2. Display the festival tree")
        print("3. Exit the festival program")

        user_choice = input().strip()
        if user_choice == '1':
            festival_tree.play_festival_game()
        elif user_choice == '2':
            print("Choose tree traversal type:")
            print("1. Preorder")
            print("2. Inorder")
            print("3. Postorder")
            traversal_choice = input("Enter your choice (1, 2, or 3): ").strip()
            if traversal_choice in ['1', '2', '3']:
                festival_tree.display_tree(festival_tree.root, traversal=('preorder', 'inorder', 'postorder')[int(traversal_choice) - 1])
            else:
                print("Invalid choice. Please try again.")
        elif user_choice == '3':
            print("Exiting the festival program.")
            break
        else:
            print("Invalid choice. Please try again.")
