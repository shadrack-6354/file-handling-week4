# file-handling-week4
const fs = require('fs');
const readline = require('readline');

// Create an interface for user input
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to read, modify, and write a file
function readAndModifyFile() {
    // Ask user for the file name
    rl.question('Please enter the filename to read: ', (filename) => {
        // Read the file asynchronously
        fs.readFile(filename, 'utf8', (err, data) => {
            if (err) {
                // Error handling: file doesn't exist or can't be read
                console.error(`Error reading file: ${err.message}`);
                rl.close();
                return;
            }
            console.log(`Original file content:\n${data}\n`);

            // Modify the content (for example, appending text)
            const modifiedContent = data + "\n\nModified content: This text was added using JavaScript!";

            // Ask the user for the output file name
            rl.question('Please enter the filename to save the modified content: ', (outputFilename) => {
                // Write the modified content to a new file
                fs.writeFile(outputFilename, modifiedContent, 'utf8', (err) => {
                    if (err) {
                        console.error(`Error writing file: ${err.message}`);
                    } else {
                        console.log(`Successfully wrote to ${outputFilename}`);
                    }
                    rl.close();
                });
            });
        });
    });
}

// Start the process
readAndModifyFile();
