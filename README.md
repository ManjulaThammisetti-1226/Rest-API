# Rest-API
from flask import Flask, request, jsonify

app = Flask(__name__)

# In-memory user storage
users = []

# GET - View all users
@app.route('/users', methods=['GET'])
def get_users():
    return jsonify(users)

# POST - Add new user
@app.route('/users', methods=['POST'])
def add_user():
    data = request.json
    users.append(data)
    return jsonify({"message": "User added successfully"}), 201

# PUT - Update user
@app.route('/users/<int:user_id>', methods=['PUT'])
def update_user(user_id):
    if user_id < len(users):
        users[user_id] = request.json
        return jsonify({"message": "User updated"})
    return jsonify({"message": "User not found"}), 404

# DELETE - Delete user
@app.route('/users/<int:user_id>', methods=['DELETE'])
def delete_user(user_id):
    if user_id < len(users):
        users.pop(user_id)
        return jsonify({"message": "User deleted"})
    return jsonify({"message": "User not found"}), 404


if __name__ == '__main__':
    app.run(debug=True)
