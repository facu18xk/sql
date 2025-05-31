# MiniSQL Engine

A lightweight, in-memory database engine with SQL-like interface built in C for learning data structures and algorithms. This project implements core database concepts using fundamental DSA components including AVL trees, splay trees, BSTs, stacks, queues, and linked lists.

## 🎯 Learning Objectives

This project is designed to provide hands-on experience with:
- **Tree Structures**: AVL trees for balanced indexing, BSTs for primary storage, Splay trees for cache optimization
- **Linear Structures**: Stacks for undo mechanisms, queues for transaction processing, linked lists for schema management
- **Database Concepts**: ACID properties, query parsing, storage engines, indexing strategies
- **Clean Architecture**: Separation of concerns, dependency inversion, testable design

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────┐
│                PRESENTATION LAYER               │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────┐ │
│  │    REPL     │  │   CLI Args  │  │   File   │ │
│  └─────────────┘  └─────────────┘  └──────────┘ │
└─────────────────────────────────────────────────┘
                         │
┌─────────────────────────────────────────────────┐
│               APPLICATION LAYER                 │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────┐ │
│  │   Parser    │  │  Validator  │  │ Executor │ │
│  └─────────────┘  └─────────────┘  └──────────┘ │
└─────────────────────────────────────────────────┘
                         │
┌─────────────────────────────────────────────────┐
│                 DOMAIN LAYER                    │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────┐ │
│  │   Entities  │  │ Use Cases   │  │Services  │ │
│  │  (Table,    │  │ (CRUD Ops)  │  │(TX Mgr)  │ │
│  │   Row, etc) │  └─────────────┘  └──────────┘ │
│  └─────────────┘                                │
└─────────────────────────────────────────────────┘
                         │
┌─────────────────────────────────────────────────┐
│              INFRASTRUCTURE LAYER               │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────┐ │
│  │  AVL Tree   │  │ Splay Tree  │  │   BST    │ │
│  │   Index     │  │   Cache     │  │ Storage  │ │
│  └─────────────┘  └─────────────┘  └──────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────┐ │
│  │    Stack    │  │    Queue    │  │  L.List  │ │
│  │   (Undo)    │  │    (TX)     │  │ (Schema) │ │
│  └─────────────┘  └─────────────┘  └──────────┘ │
└─────────────────────────────────────────────────┘
```

## 🚀 Features

### Core Database Operations
- **DDL**: `CREATE TABLE`, `DROP TABLE`, `ALTER TABLE`
- **DML**: `INSERT`, `SELECT`, `UPDATE`, `DELETE`
- **TCL**: `BEGIN`, `COMMIT`, `ROLLBACK`
- **Schema Management**: Column types (INT, TEXT, REAL), constraints, primary keys

### Data Structure Integration
- **AVL Trees**: Self-balancing binary search trees for primary key indexing
- **Splay Trees**: Self-adjusting trees for frequently accessed data optimization
- **BST**: Basic binary search trees for secondary indexing
- **Stacks**: LIFO structure for undo operations and transaction rollback
- **Queues**: FIFO structure for transaction processing and command buffering  
- **Linked Lists**: Dynamic arrays for schema definitions and result sets

### Advanced Features
- **ACID Transactions**: Atomicity, Consistency, Isolation, Durability
- **Query Optimization**: Index-based lookups, query plan caching
- **Memory Management**: Custom allocators, garbage collection
- **Concurrent Access**: Basic locking mechanisms (future enhancement)

## 📁 Project Structure

```
minisql/
├── src/
│   ├── presentation/           # User interface layer
│   │   ├── repl.c             # Interactive shell
│   │   ├── cli.c              # Command line interface
│   │   └── file_loader.c      # SQL file execution
│   ├── application/           # Application services
│   │   ├── parser/            # SQL parsing
│   │   │   ├── lexer.c
│   │   │   ├── parser.c
│   │   │   └── ast.c
│   │   ├── validator.c        # Input validation
│   │   └── executor.c         # Command execution
│   ├── domain/               # Business logic
│   │   ├── entities/         # Core entities
│   │   │   ├── table.c
│   │   │   ├── row.c
│   │   │   ├── column.c
│   │   │   └── schema.c
│   │   ├── usecases/         # Business operations
│   │   │   ├── crud_ops.c
│   │   │   ├── transaction.c
│   │   │   └── query_ops.c
│   │   └── services/         # Domain services
│   │       ├── tx_manager.c
│   │       └── index_manager.c
│   └── infrastructure/       # Data structures & I/O
│       ├── data_structures/  # Core DSA implementations
│       │   ├── avl_tree.c
│       │   ├── splay_tree.c
│       │   ├── bst.c
│       │   ├── stack.c
│       │   ├── queue.c
│       │   └── linked_list.c
│       ├── storage/          # Storage engine
│       │   ├── memory_mgr.c
│       │   ├── page_mgr.c
│       │   └── buffer_pool.c
│       └── persistence/      # File I/O (optional)
│           ├── file_io.c
│           └── serializer.c
├── include/                  # Header files
│   ├── presentation/
│   ├── application/
│   ├── domain/
│   └── infrastructure/
├── tests/                    # Unit tests
│   ├── unit/
│   ├── integration/
│   └── performance/
├── examples/                 # Sample SQL files
│   ├── basic_crud.sql
│   ├── transactions.sql
│   └── complex_queries.sql
├── docs/                     # Documentation
│   ├── architecture.md
│   ├── dsa_usage.md
│   ├── api_reference.md
│   └── performance_analysis.md
├── scripts/                  # Build and utility scripts
│   ├── build.sh
│   ├── test.sh
│   └── benchmark.sh
├── Makefile
├── CMakeLists.txt           # Alternative build system
└── README.md
```

## 🗺️ Development Roadmap

### Phase 1: Foundation & Core CRUD 
**Goal**: Basic functionality with essential data structures
- [ ] Implement core data structures (linked list, stack, queue)
- [ ] Basic BST for primary storage
- [ ] Simple parser for CREATE, INSERT, SELECT
- [ ] REPL interface with basic commands
- [ ] Memory management foundation

**DSA Focus**: Linked lists, stacks, basic BST operations

### Phase 2: Balanced Trees & Indexing 
**Goal**: Efficient data access and storage
- [ ] AVL tree implementation for primary key indexing
- [ ] Self-balancing operations (rotations, rebalancing)
- [ ] Index-based SELECT operations
- [ ] DELETE operations with tree restructuring
- [ ] Performance benchmarking tools

**DSA Focus**: AVL trees, tree rotations, balance factors

### Phase 3: Transactions & Undo Mechanism 
**Goal**: ACID properties and rollback functionality
- [ ] Transaction state management using stacks
- [ ] BEGIN, COMMIT, ROLLBACK commands
- [ ] Undo log implementation
- [ ] Nested transaction support
- [ ] Deadlock detection basics

**DSA Focus**: Stacks for undo operations, state management

### Phase 4: Advanced Querying & UPDATE 
**Goal**: Complex query processing
- [ ] WHERE clause parsing and evaluation
- [ ] UPDATE operations with indexing
- [ ] Query optimization using trees
- [ ] Range queries and tree traversals
- [ ] Multi-column indexing

**DSA Focus**: Tree traversals, search optimization

### Phase 5: Splay Trees & Caching 
**Goal**: Performance optimization for frequently accessed data
- [ ] Splay tree implementation
- [ ] Cache replacement policies
- [ ] Adaptive data structure selection
- [ ] Performance comparison: AVL vs Splay vs BST
- [ ] Access pattern analysis

**DSA Focus**: Splay trees, self-adjusting structures

### Phase 6: Advanced Features 
**Goal**: Production-ready features
- [ ] Persistence layer (save/load to disk)
- [ ] JOIN operations using hash tables
- [ ] Concurrent access with basic locking
- [ ] Memory optimization and garbage collection
- [ ] Comprehensive error handling

**DSA Focus**: Hash tables, queue-based scheduling

## 📊 Data Structure Usage Map

| Component | Primary DS | Secondary DS | Purpose |
|-----------|------------|--------------|---------|
| **Storage Engine** | AVL Tree | BST | Balanced primary key indexing |
| **Cache Layer** | Splay Tree | - | Optimize frequent access patterns |
| **Transaction Log** | Stack | Queue | Undo operations, command buffering |
| **Schema Management** | Linked List | - | Dynamic schema definitions |
| **Query Results** | Linked List | - | Dynamic result set storage |
| **Index Management** | BST | AVL Tree | Secondary indexes |
| **Memory Pool** | Stack | Linked List | Memory allocation tracking |

## 🎯 Success Metrics

By completing this project, you should be able to:
- [ ] Implement and explain AVL tree rotations and balancing
- [ ] Design and implement a transaction system using stacks
- [ ] Optimize data access patterns using splay trees
- [ ] Parse and execute SQL-like commands
- [ ] Apply clean architecture principles in C
- [ ] Analyze time/space complexity of operations
- [ ] Debug memory issues in C programs
- [ ] Design efficient indexing strategies

-
