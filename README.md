# PRODIGY_CS_03
import re

def assess_password_strength(password):
    strength = 0
    feedback = []
    
    # Criteria checks
    length_criteria = len(password) >= 8
    uppercase_criteria = bool(re.search(r"[A-Z]", password))
    lowercase_criteria = bool(re.search(r"[a-z]", password))
    number_criteria = bool(re.search(r"\d", password))
    special_criteria = bool(re.search(r"[!@#$%^&*(),.?\":{}|<>]", password))
    
    # Strength calculation
    if length_criteria:
        strength += 2
    else:
        feedback.append("Increase password length to at least 8 characters.")
    
    if uppercase_criteria:
        strength += 1
    else:
        feedback.append("Add at least one uppercase letter.")
    
    if lowercase_criteria:
        strength += 1
    else:
        feedback.append("Add at least one lowercase letter.")
    
    if number_criteria:
        strength += 1
    else:
        feedback.append("Include at least one number.")
    
    if special_criteria:
        strength += 1
    else:
        feedback.append("Use at least one special character (e.g., !, @, #, etc.).")
    
    # Strength feedback
    if strength <= 2:
        strength_label = "Weak"
    elif strength <= 4:
        strength_label = "Moderate"
    else:
        strength_label = "Strong"
    
    return {
        "strength": strength_label,
        "score": strength,
        "feedback": feedback
    }

# Example usage
password = input("Enter a password: ")
result = assess_password_strength(password)
print(f"Password Strength: {result['strength']} (Score: {result['score']}/6)")
for tip in result['feedback']:
    print(f"- {tip}")
