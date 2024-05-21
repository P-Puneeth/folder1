# folder1
CREATE TABLE Members (
    MemberID NUMBER PRIMARY KEY,
    FirstName VARCHAR2(50) NOT NULL,
    LastName VARCHAR2(50) NOT NULL,
    Email VARCHAR2(100) NOT NULL UNIQUE,
    Phone VARCHAR2(15) NOT NULL,
    JoinDate DATE NOT NULL,
    MembershipType VARCHAR2(20) NOT NULL CHECK (MembershipType IN ('Standard', 'Premium', 'VIP'))
);

CREATE TABLE Books (
    BookID NUMBER PRIMARY KEY,
    Title VARCHAR2(200) NOT NULL,
    Author VARCHAR2(100) NOT NULL,
    Publisher VARCHAR2(100) NOT NULL,
    PublishedYear NUMBER(4) NOT NULL,
    ISBN VARCHAR2(13) NOT NULL UNIQUE,
    Category VARCHAR2(50) NOT NULL,
    CopiesAvailable NUMBER NOT NULL
);

CREATE TABLE Loans (
    LoanID NUMBER PRIMARY KEY,
    MemberID NUMBER NOT NULL,
    BookID NUMBER NOT NULL,
    LoanDate DATE NOT NULL,
    DueDate DATE NOT NULL,
    ReturnDate DATE NULL,
    Status VARCHAR2(20) NOT NULL CHECK (Status IN ('On Loan', 'Returned')),
    FOREIGN KEY (MemberID) REFERENCES Members(MemberID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID)
);

CREATE TABLE Categories (
    CategoryID NUMBER PRIMARY KEY,
    CategoryName VARCHAR2(50) NOT NULL UNIQUE
);

-- Optionally, ensure that the Categories exist before they can be referenced
ALTER TABLE Books
ADD CONSTRAINT fk_category
FOREIGN KEY (Category)
REFERENCES Categories (CategoryName);
