# PLP-Python-assignment-week-5
def file_processor():
    """Reads a file, transforms its content, and writes to a new file with comprehensive error handling."""
    while True:
        try:
            # Get file paths from user
            source_path = input("Enter the source file path: ").strip()
            dest_path = input("Enter the destination file path: ").strip()

            # Verify destination is different from source
            if source_path == dest_path:
                raise ValueError("Destination file cannot be the same as source file")

            # Read and process file
            with open(source_path, 'r', encoding='utf-8') as src_file:
                content = src_file.read()
                modified_content = transform_content(content)

            # Write to new file
            with open(dest_path, 'w', encoding='utf-8') as dest_file:
                dest_file.write(modified_content)

            print(f"\nSuccess! Modified content written to {dest_path}")
            break

        except FileNotFoundError:
            print("\nError: The specified file was not found. Please try again.")
        except PermissionError:
            print("\nError: You don't have permission to access this file.")
        except UnicodeDecodeError:
            print("\nError: Could not read the file (possibly a binary file).")
        except ValueError as ve:
            print(f"\nError: {ve}")
        except Exception as e:
            print(f"\nAn unexpected error occurred: {str(e)}")
        
        # Offer retry option
        retry = input("\nWould you like to try again? (y/n): ").lower()
        if retry != 'y':
            print("Operation cancelled.")
            break

def transform_content(content):
    """Example transformation function (customize as needed)."""
    # Current transformation: capitalize each line
    return '\n'.join(line.capitalize() for line in content.splitlines())

if __name__ == "__main__":
    print("=== File Content Transformer ===")
    print("This program reads a file, transforms its content,")
    print("and saves the modified version to a new file.\n")
    file_processor()
