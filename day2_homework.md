<h1>SQL Property Tracker Quiz</h1>
<h2>MVP Questions</h2>
In our Property Tracker application:<br>
<br>
<strong>Q1. Where are we instantiating instances of the Property class?</strong>

<em>We are instantiating instances of the Property class in our test files (console.rb and property_spec.rb), or when we need to convert a PG::Result object to a Property object.</em>

<strong>Q2. Where are we defining the SQL that enables us to save the ruby Property object into the database?</strong>

<em>The table schema is defined in the SQL file in the db folder and the SQL CRUD actions are defined in the methods in the Property class file.</em>

<strong>Q3. In console.rb, which lines modify the database?</strong>

<em>Property.delete_all() and property1.save().</em>

<strong>Q4. Why do we not define the id of a Property object at the point we instantiate it (‘new it up’)?</strong>

<em>An id is only assigned once the object has been added to the database so we don't know the id at instantiation.</em>

<strong>Q5. Where and how do we assign the id (that is generated by the database) to the ruby Property object?</strong>

<em>In our save() method inside the Property class, we use 'RETURNING id' at the end of the SQL statement, access the value of the 'id' key in the output, convert this to an integer and assign to the @id instance variable of the Property object.</em>

<strong>Q6. Why do we put a guard (an if clause) on the @id attribute in the constructor?</strong>

<em>Allows us to instantiate a new Property object with or without an id (i.e. before or after the object has been added to the database).</em>

<strong>Q7. Why are some of the CRUD actions represented by instance methods, and others by class methods?</strong>

<em>Some actions are 'global' in the sense that they need to work on all of the Property objects in a database, so are represented by class methods. Other actions act on specific instances of the Property class so can be represented by instance methods.</em>

<strong>Q8. What type of data structure is returned by calls to db.exec_prepared()? In the save method, how do we access the id from the returned data structure?</strong>

<em>db.exec_prepared() returns an array of hashes, and we access the id using result[0]['id'].</em>

<strong>Q9. Why do we use prepared statements when performing database operations?</strong>

<em>To sanity check the inputs and to guard against SQL injection attacks which could corrupt or destroy the database.</em>

<h2>Extension Questions</h2>
Look at the find_by_id and find_by_address methods in the Property class.

<strong>Q10. What do they take in as their arguments?</strong>

<em>They take in an id or an address, which can be passed to the db.exec_prepared() method as values for a SELECT sql statement.</em>

<strong>Q11. What are their return values?</strong>

<em>The return values are PG::Result objects which take the form of hashes containing the retrieved data in String format. These can be converted to Property objects using the map method and Property.new.</em>
