# CSE 344 Midterm Review

* Databases

    * Database: Collection of files storing <b>related data</b>.
    * Database Management System: an application program that allows us to manage efficiently the collection of data files.
    * Responsibility of DBMS:
        * Data storage and manipulation
        * Black box throught
        * Physical data independence

* Relational Databases

    * Motivation: avoid singular/flat files
    * Data Model: <b>Mathematical/Conceptual</b> way for decribling the data
        * Schemas and keys
        * Record and attributes
        * Attribute types/typing
    
        Three elements of data models:
        * Instance (actual data)
        * Schema (what data being stored)
        * Query language (how to retrieve qnd manipulate data)
    
    * Keys: one (or more) attributes that <b>uniquely identify</b> a record
        * When multiple keys, we can choose one key as <b>primary key</b>.
    * Foreign keys: attributes whose value is a key of a record in some other relation.

    * SQL Structure:
        * Flat tables:
            * First normal form
            * Crosswalks and joins
            * Breaking up data into multiple relations

            Tables are <b>not ordered</b>, <b>flat</b>, and has <b>physical data independence</b> (do not prescribe how they are implemented/stored on disk).
        
        * Code:
            * <code>create</code> statements: declaring <b>types</b> and <b>keys</b>.
            * <code>insert</code>/<code>delete</code> statements
            * <code>update</code>
            * <code>drop</code> table

        * <code><b>DISTINCT</b></code>: return unique elements<br />
            <b>Projection</b>: function which selects a subset of the attributes
        
        * Inner vs. Outer Joining
            * <b>inner joining</b>: each row must come from both tables
            * <b>outer joining</b>: include rows from only one of the two tables
            * <code>tableA (left/right/full) outer join tableB</code>:
                *  Left outer join: includes tuples from <code>tableA</code> even if no match
                *  Right outer join: includes tuples from <code>tableB</code> even if no match
                *  Full outer join: includes tuples from both <code>tableA</code> and <code>tableB</code> even if no match
        
        * Nested loop semantics
            * Cross-join multiple tables with selection

        * Self joins
            * includes one table multiple times
        
        * Aggregation:
            * Everything in <code>SELECT</code> must be either a <b>GROUP-BY</b> attribute, ot an aggregate.
        
        * <code>WHERE</code> vs. <code>HAVING</code>:
            * <code>WHERE</code> can contain any condition on attributes in <code>FROM</code> clause.
                * Applied to individual rows.
                * No aggregate.
            * <code>HAVING</code> can contain any condition on aggregate expressions and any group-by keys.
                * Entire group is returned, or removed.

        * Executing in order of: <b>FWGHOS</b>

        * Subqueries:
            * In <code>SELECT</code>: single attribute projection
            * In <code>FROM</code>: use <code>AS</code> and <code>WITH AS</code>
            * In <code>WHERE</code>: use <b>existential quantifiers</b> (<code>EXISTS</code>, <code>IN</code>, <code>ANY</code>, <code>ALL</code>)
            * <b>Correlated</b> subquery: depends on outside query.
            * Finding Witness (the product with max price): compute aggregate in subquery.
        
        * Monotonicity:
            * A query is <b>monotone</b> if whenever we add tuples to one or more input tables, the answer to the query will not lose any of the tuples.
            * If Q is a <code>SELECT-FROM-WHERE</code> query that <b>does not</b> involve any subqueries, Q <b>is</b> monotone.
            * Queries with <b>universal quantifiers</b>(all) or <b>negation</b> must be nested.
    
    * Relational Algebra:
        * Set/Bag semantics: differs on allowing/disallowing duplicates in tuples, also referred as "Standard"/"Extended" Relational Algebra

        * Operators:
            * Union $\cup$, intersection $\cap$, difference $-$
            * selection $\sigma$
            * projection $\pi$
            * Cartesian product $\times$, join $\bowtie$
            * Rename $\rho$
            * Duplicate elimination $\delta$
            * Grouping and aggregation $\gamma$
            * sorting $\tau$

            All operators take 1 or more relations as input and return another relation.

            Join in R.A.:
            * <b>Theta-join</b>: $R \bowtie_{\theta} S = \sigma_{\theta} (R \times S)$
            * <b>Equijoin</b>: Theta-joins which join condition $\theta$ only involves equilities.
            * <b>Natural Join</b>: $R \bowtie S = \pi_A(\sigma_\theta(R \times S))$

        * Relational Algebra is <b>equally expressive</b> with SQL.
    
    * Datalog:
        * For Queries that cannot be defined in RA (recursive queries)
        * Terminology:
            * Facts: tuples in database
            * Rules: queries
            * Extensional Predicates: predicates defined in database itself
            * Intensional Predicates: self-defined predicates
            * Head: the intensional predicates to be defined
            * Body: rule for each head (made with atoms/relational predicates)
            * head variables / existential variables
        * Fixpoint semantics: start with empty relations, repeat until $IDB_t = IDB_{t + 1}$.
            * A datalog program without functions (+, *, ...) always terminates in polynomial time.
        * Minimal model semantics: returns the smallest IDB such that all vars in EDB satisfies rule defined for this IDB (recursively too).
        * Linear:
            * Right-linear: <code>T(x, y) :- R(x, z), T(z, y)</code>
            * Left-linear: <code>T(x, y) :- T(x, z), R(z, y)</code>
            * Non-linear: <code>T(x, y) :- T(x, z), T(z, y)</code>
        * Writing Rules:
            * Safe: if every variable appears in some positive relational atom

* Semi-structured Data

    * Transactional Data: Frequent read, simple update
    * Analytical Data: Decision support, multiple joins & group bys
    * Partitioning: Store data partitioned on multiple servers, easy to write, hard to read
    * Dupplication: Duplicate data on multiple files, hard to write, easy to read