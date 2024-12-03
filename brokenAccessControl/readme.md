Broken Access Control occurs when a system fails to properly enforce restrictions on what authenticated users can do. In other words, users can perform actions they shouldn't be allowed to do.

    # Vulnerable code example
    @app.route('/user_profile/<user_id>')
    def view_profile(user_id):
        # No authentication check!
        user_data = db.query(f"SELECT * FROM users WHERE id = {user_id}")
        return render_template('profile.html', data=user_data)

    # Secure version
    @app.route('/user_profile/<user_id>')
    @login_required
    def view_profile(user_id):
        if current_user.id != user_id and not current_user.is_admin:
            return abort(403)  # Forbidden
        user_data = db.query(f"SELECT * FROM users WHERE id = {user_id}")
        return render_template('profile.html', data=user_data)

My Experience

- Understanding the business process of your apps and then when you create a new row in database always questioning who will gained access to read, update, and delete the row.
