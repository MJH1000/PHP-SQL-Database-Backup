<?php
/**
 * PHP SQL Database Backup
 *
 * @author Michael Hochkins
 */

// Database configuration
$host     = 'localhost';
$username = 'root';
$password = 'password';
$dbname   = 'database';

// Backup settings
$backupDir = './database_backups/'; // Directory where backups are saved
$backupFilePrefix = $dbname . '_backup_'; // Prefix for backup filenames
$backupFileExtension = '.sql.gz'; // Extension for compressed backup files

// Create backup directory if it doesn't exist
if (!is_dir($backupDir)) {
    mkdir($backupDir, 0775, true);
}

// Function to generate the current timestamp for the filename
function getCurrentTimestamp() {
    return date('Y-m-d_H-i-s');
}

// Generate the full path for the backup file
$backupFilePath = $backupDir . $backupFilePrefix . getCurrentTimestamp() . $backupFileExtension;

// Command to export the database using mysqldump
$dumpCommand = "mysqldump -h{$host} -u{$username} -p{$password} {$dbname} | gzip > {$backupFilePath}";

try {
    // Execute the command and check its success
    $output = null;
    $resultCode = null;
    exec($dumpCommand, $output, $resultCode);

    if ($resultCode === 0) {
        echo "<h1>Database backup successful</h1><p>Download: <a target=\"_blank\" href=\"{$backupFilePath}\">{$backupFilePath}</a></p>";
    } else {
        throw new Exception("Backup failed with error code: {$resultCode}");
    }
} catch (Exception $e) {
    echo "An error occurred during backup: " . $e->getMessage() . "\n";
}
