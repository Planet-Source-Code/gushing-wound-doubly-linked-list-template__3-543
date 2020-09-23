<div align="center">

## Doubly Linked List Template


</div>

### Description

Template for a doubly linked-list data structure, can be used also for queues and stacks.
 
### More Info
 
Template argument: RecordClass

the class that will be stored in the list.

A template class for a doubly-linked list. This list will allocate and deallocate

internal memory, so ensure that callers of this class are using the same memory heap.

However, the items that are passed to this linked-list template will not be deleted

at any time by this template. Who ever allocates the memory is responsible for deallocating,

but note that if this memory is deallocated while still being used by this list class, then

you are asking for trouble.

Internally, this list will create a doubly linked list by creating an external

node to point to you items. It looks a little something like...



----



----



----

| MyClass |    | MyClass |    | MyClass |



----



----



----

^          ^          ^

| (pointer to)   |          |

|          |          |

|          |          |



----



----



----

| Internal.|<

----

>| Internal.|<

----

>| Internal.|<

----

> \\



----



----



----

This file declares three template classes which operate together to implement

the class file. Note that these classes should be defined in the same file since

the C++ 'friend' modifier was used. As a result, the CTL_DoublyLinkedListIterator and the

RecordInterface classes should be considered to be part of the interface of the

CTL_DoublyLinkedList, and therefore should be defined in the same file to avoid 'long-distance

friendships' (as per the literature).

The following is an example of how to use this template.

----

*	CTL_DoublyLinkedList<TestRecord> list;

*	CTL_DoublyLinkedList<TestRecord>::Iterator it;

*	TestRecord a[10];

*	int i;

*

*	// initialize data

*	for (i=0; i<10; i++)

*	{

*		a[i].data1=i*10;

*		a[i].data2=i*100;

*	}

*

*	list.addRecord( &a[9] );

*	list.addRecord( &a[4] );

*	list.addRecord( &a[3] );

*	list.addRecord( &a[2] );

*	list.addRecord( &a[8] );

*

*	printf( "Displaying records: 9,4,3,2,8\n" );

*	for (it=list; it(); ++it)

*		printf( "record: %d, %d\n", it()->data1, it()->data2 );

----

The following template classes defined in this file:

CTL_DoublyLinkedList<MyClass>

CTL_DoublyLinkedList<MyClass>::Iterator

Does not manipulate, allocate, or deallocate records. Does allocate and deallocate nodes that point to the records that are added to the list.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Gushing Wound](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/gushing-wound.md)
**Level**          |Advanced
**User Rating**    |4.5 (18 globes from 4 users)
**Compatibility**  |C, C\+\+ \(general\)
**Category**       |[Data Structures](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/data-structures__3-8.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/gushing-wound-doubly-linked-list-template__3-543/archive/master.zip)





### Source Code


/**
 * File:		ctl_doublylinkedlist.h
 * Author:		Corey Ippolito
 * Date:		April 2000
 * Email:		ippolito@isye.gatech.edu
 *
 * This file contains the template class for a doubly-linked list.
 *
 * The following template classes defined in this file:
 *  CTL_DoublyLinkedList<MyClass>
 *  CTL_DoublyLinkedList<MyClass>::Iterator
 *  CTL_DoublyLinkedList<MyClass>::NodeInterface
 *
 *
 */
#ifndef INCLUDED_CTL_DOUBLYLINKEDLIST_H
#define INCLUDED_CTL_DOUBLYLINKEDLIST_H
#include "ctldefs.h"
#include <stdio.h>
/**
 * <FONT FACE="Arial">Template for the linked-list class and implementation.
 *
 * <FONT FACE="Arial">
 * A template class for a doubly-linked list. This list will allocate and deallocate
 * internal memory, so ensure that callers of this class are using the same memory heap.
 * However, the items that are passed to this linked-list template will not be deleted
 * at any time by this template. Who ever allocates the memory is responsible for deallocating,
 * but note that if this memory is deallocated while still being used by this list class, then
 * you are asking for trouble.
 *
 * Internally, this list will create a doubly linked list by creating an external
 * node to point to you items. It looks a little something like...
 *
 *<pre>
 *   ------------    ------------    ------------
 *   | MyClass |    | MyClass |    | MyClass |
 *   ------------    ------------    ------------
 *     ^          ^          ^
 *     | (pointer to)   |          |
 *     |          |          |
 *     |          |          |
 *   ------------    ------------    ------------
 *   | Internal.|<------>| Internal.|<------>| Internal.|<------> \\
 *   ------------    ------------    ------------
 *</pre>
 *
 *
 * This file declares three template classes which operate together to implement
 * the class file. Note that these classes should be defined in the same file since
 * the C++ 'friend' modifier was used. As a result, the CTL_DoublyLinkedListIterator and the
 * RecordInterface classes should be considered to be part of the interface of the
 * CTL_DoublyLinkedList, and therefore should be defined in the same file to avoid 'long-distance
 * friendships' (as per the literature).
 *
 * The following is an example of how to use this template.
 *
 * <pre>
 * ---------------------------------------------------
 *	CTL_DoublyLinkedList<TestRecord> list;
 *	CTL_DoublyLinkedList<TestRecord>::Iterator it;
 *	TestRecord a[10];
 *	int i;
 *
 *	// initialize data
 *	for (i=0; i<10; i++)
 *	{
 *		a[i].data1=i*10;
 *		a[i].data2=i*100;
 *	}
 *
 *	list.addRecord( &a[9] );
 *	list.addRecord( &a[4] );
 *	list.addRecord( &a[3] );
 *	list.addRecord( &a[2] );
 *	list.addRecord( &a[8] );
 *
 *	printf( "Displaying records: 9,4,3,2,8\n" );
 *	for (it=list; it(); ++it)
 *		printf( "record: %d, %d\n", it()->data1, it()->data2 );
 * ---------------------------------------------------
 * </pre>
 *
 * The following template classes defined in this file:
 *  CTL_DoublyLinkedList<MyClass>
 *  CTL_DoublyLinkedList<MyClass>::Iterator
 */
template <class RecordClass> class CTL_DoublyLinkedList
{
	public:
		// constructor/destructor
		CTL_DoublyLinkedList();
		~CTL_DoublyLinkedList();
		/** IMPORTANT! The copy iterator will copy the list by allocating new internal nodes
		 * that point to the SAME records that the other list points to. I.E., don't delete
		 * that data unless you remove the record first from both lists. */
		void	operator = ( CTL_DoublyLinkedList<RecordClass>& copyList );
		/** returns the number of records in the list */
		int				getNumberOfRecords(void);
		/** returns the requested record in O(n) time */
		RecordClass*	getRecord( int recordID );
		/** determines if the item is a member of the list */
		Boolean			isElement( RecordClass* lprecord );
		// ---- list manipulation interface
		/**
		 * Clears the linked list, resets to an empty list
		 *
		 * This method clears the list to an empty list. The internal
		 * data is deallocated, but the records that the list was
		 * pointing to is not!
		 */
		void	clearList(void);
		/** adds the record to the list */
		int		addRecord( RecordClass* lpRecord );
		/** adds the record to the list and ensures there is only one of the elements in the list */
		void addRecordUnrepeated( RecordClass* lpRecord );
		/** adds the record to the start of the list */
		int		addRecordToStart( RecordClass* lpRecord );
		/** adds the record to the end of the list */
		int		addRecordToEnd( RecordClass* lpRecord );
		/** removes and returns the recordID'th record from the list */
		RecordClass*	removeRecord( int recordID );
		/** removes the specified record from the list */
		RecordClass*	removeRecord( RecordClass* lpRemoveNode );
		/** removes the first record from the list */
		RecordClass*	removeFirstRecord(void);
		/** removes the last record from the list */
		RecordClass*	removeLastRecord(void);
		/** moves the specified record up one position in the list */
		void	promoteRecord(RecordClass* lpRecordToPromote );
		/** moves the specified record down one position in the list */
		void	demoteRecord(RecordClass* lpRecordToDemote );
	private:
		struct RecordClassNode
		{
			RecordClass*		m_lpRecord;
			RecordClassNode*	m_lpNext;
			RecordClassNode*	m_lpPrevious;
		};
		RecordClassNode*	m_lpRoot;
		int					m_numberOfRecords;
		// protected helper functions
		RecordClassNode*	f_getLastRecordNode(void);
		RecordClassNode*	f_getRecordNode( int recordID );
	public:
		/**
		 *<FONT FACE="Arial"> Iterator class to access elements in the CTL_DoublyLinkedList
		 *
		 * Iterator to access the elements of the CTL_DoublyLinkedList. The following
		 * example shows how to use this class.
		 *
		 * <pre>
		 * ---------------------------------------------------
		 * class MyRecord;
		 *	CTL_DoublyLinkedList<MyRecord> list;
		 *	CTL_DoublyLinkedList<MyRecord>::Iterator iter;
		 *
		 * // ....
		 *
		 *	for (iter=list; iter(); ++iter)
		 *	{
		 *   // access iter()
		 * }
		 * ---------------------------------------------------
		 * </pre>
		 *
		 */
		class Iterator
		{
			public:
				Iterator( )
				{
					lpCurrent = NULL;
				};
				/** Points the iterator to the first record in the list */
				inline void operator=(CTL_DoublyLinkedList<RecordClass> &src)
				{
					lpCurrent = src.m_lpRoot;
				};
				/** Copy the location of another iterator */
				inline void operator=(Iterator &copyIt)
				{
					lpCurrent = copyIt.lpCurrent;
				};
				friend Iterator;
				/** Moves to the next record */
				inline void operator++(void)
				{
					if (lpCurrent != NULL)
						lpCurrent = lpCurrent->m_lpNext;
				};
				/** Moves to the previous record */
				inline void operator--(void)
				{
					if (lpCurrent != NULL)
						lpCurrent = lpCurrent->m_lpPrevious;
				};
				/** Peek at the next record */
				inline RecordClass* peekAtNext(void)
				{
					if (lpCurrent != NULL)
						if (lpCurrent->m_lpNext != NULL)
							return lpCurrent->m_lpNext->m_lpRecord;
					return NULL;
				};
				/** Peek at the previous record */
				inline RecordClass* peekAtPrevious(void)
				{
					if (lpCurrent != NULL)
						if (lpCurrent->m_lpPrevious != NULL)
							return lpCurrent->m_lpPrevious->m_lpRecord;
					return NULL;
				};
				/** Returns the current record being accessed */
				inline RecordClass* operator()()
				{
					if (lpCurrent == NULL)
						return NULL;
					return lpCurrent->m_lpRecord;
				};
				/** Clears the content of the iterator */
				inline void clear()
				{
					lpCurrent = NULL;
				};
			protected:
				RecordClassNode* lpCurrent;
		};
		/** allow our iterator class to access our internals */
		friend void Iterator::operator=(CTL_DoublyLinkedList<RecordClass> &src);
};
// -------------------------------------------------------
// ---- implementation of the CTL_DoublyLinkedList class
// --------------------------------------------------------
// constructor/destructor
template <class RecordClass>
CTL_DoublyLinkedList<RecordClass>::CTL_DoublyLinkedList()
{
	m_lpRoot = NULL;
	m_numberOfRecords = 0;
}
template <class RecordClass>
CTL_DoublyLinkedList<RecordClass>::~CTL_DoublyLinkedList()
{
	clearList();
}
template <class RecordClass>
CTL_DoublyLinkedList<RecordClass>::RecordClassNode* CTL_DoublyLinkedList<RecordClass>::f_getLastRecordNode(void)
{
	int nodeCounter = 0;
	RecordClassNode* lpRecordNode = m_lpRoot;
	if (m_lpRoot == NULL)
		return NULL;
	while (lpRecordNode->m_lpNext != NULL)
	{
		nodeCounter++;
		lpRecordNode = lpRecordNode->m_lpNext;
	}
	// do an error checking here
	if (m_numberOfRecords != nodeCounter+1)
	{
		m_numberOfRecords = nodeCounter+1;
		fprintf(stderr, "*****WARNING! CTL_DoublyLinkedList has lost count!\n");
	}
	return lpRecordNode;
}
// record access interface
template <class RecordClass>
int CTL_DoublyLinkedList<RecordClass>::getNumberOfRecords(void)
{
	return m_numberOfRecords;
}
template <class RecordClass>
void CTL_DoublyLinkedList<RecordClass>::operator = ( CTL_DoublyLinkedList<RecordClass>& copyList )
{
	Iterator it;
	clearList();
	for (it = copyList; it(); ++it)
	{
		addRecordToEnd( it() );
	}
}
template <class RecordClass>
CTL_DoublyLinkedList<RecordClass>::RecordClassNode* CTL_DoublyLinkedList<RecordClass>::f_getRecordNode( int recordID )
{
	if (recordID <= 0)
	{
		if (m_lpRoot == NULL)
			return NULL;
		return m_lpRoot;
	}
	else if (recordID > m_numberOfRecords-1)
		return NULL;
	int nodeCounter = 0;
	RecordClassNode* lpRecordNode = m_lpRoot;
	while (nodeCounter < recordID && lpRecordNode != NULL)
	{
		nodeCounter++;
		lpRecordNode = lpRecordNode->m_lpNext;
	}
	// error checking
	if (lpRecordNode == NULL)
	{
		fprintf(stderr, "WARNING!- SFC Library\n   Class CTL_DoublyLinkedList (a linked-list structure) has lost count of its list.\n");
		m_numberOfRecords = nodeCounter;
	}
	return lpRecordNode;
}
template <class RecordClass>
RecordClass* CTL_DoublyLinkedList<RecordClass>::getRecord( int recordID )
{
	RecordClassNode *lpNode = f_getRecordNode(recordID);
	if (lpNode == NULL)
		return NULL;
	else
		return lpNode->m_lpRecord;
}
template <class RecordClass>
Boolean CTL_DoublyLinkedList<RecordClass>::isElement( RecordClass* lpRecord )
{
	RecordClassNode *lpNode = m_lpRoot;
	while (lpNode != NULL)
	{
		if (lpRecord == lpNode->m_lpRecord)
			return TRUE;
		lpNode = lpNode->m_lpNext;
	}
	return FALSE;
}
// list manipulation interface
template <class RecordClass>
void CTL_DoublyLinkedList<RecordClass>::clearList( void )
{
	while( removeFirstRecord() )
	{
	}
}
template <class RecordClass>
void CTL_DoublyLinkedList<RecordClass>::addRecordUnrepeated( RecordClass* lpRecord )
{
	if (lpRecord == NULL)
		return;
	// remove existing copies
	RecordClassNode* lpNode = m_lpRoot;
	Boolean alreadyExists = FALSE;
	while (lpNode != NULL)
	{
		if (lpNode->m_lpRecord == lpRecord)
		{
			if (alreadyExists==TRUE)
			{
				// we already found an occurance- lets delete this one
				removeRecord(lpNode->m_lpRecord);
				// must be a better way to do this, but lets go ahead and reset to the beginning
				// of the list and try again
				alreadyExists = FALSE;
				lpNode = m_lpRoot;
			}
			else
			{
				alreadyExists = TRUE;
				lpNode = lpNode->m_lpNext;
			}
		}
		else
			lpNode = lpNode->m_lpNext;
	}
	// did we find it? If not, then add it
	if (alreadyExists == FALSE)
		addRecordToStart(lpRecord);
}
template <class RecordClass>
int CTL_DoublyLinkedList<RecordClass>::addRecord( RecordClass* lpRecord )
{
	return addRecordToEnd(lpRecord);
}
template <class RecordClass>
int CTL_DoublyLinkedList<RecordClass>::addRecordToStart( RecordClass* lpRecord )
{
	if (lpRecord == NULL) return -1;
	// create node for record
	RecordClassNode* lpNode = new RecordClassNode;
	lpNode->m_lpRecord = lpRecord;
	// add to the beginning
	lpNode->m_lpNext = m_lpRoot;
	lpNode->m_lpPrevious = NULL;
	if ( m_lpRoot != NULL )
	{
		m_lpRoot->m_lpPrevious = lpNode;
	}
	m_lpRoot = lpNode;
	m_numberOfRecords++;
	return 0;
}
template <class RecordClass>
int CTL_DoublyLinkedList<RecordClass>::addRecordToEnd( RecordClass* lpRecord )
{
	if (lpRecord == NULL) return -1;
	if (m_lpRoot == NULL)
		return addRecordToStart(lpRecord);
	else
	{
		// create a new record struct
		RecordClassNode*	lpStruct = new RecordClassNode;
		lpStruct->m_lpRecord = lpRecord;
		// get last record node
		RecordClassNode *lpInsertPtr = f_getLastRecordNode();
		// insert after last node
		lpInsertPtr->m_lpNext = lpStruct;
		lpStruct->m_lpPrevious = lpInsertPtr;
		lpStruct->m_lpNext = NULL;
		m_numberOfRecords++;
	}
	return m_numberOfRecords-1;
}
template <class RecordClass>
RecordClass* CTL_DoublyLinkedList<RecordClass>::removeRecord( int recordID )
{
	if (m_lpRoot == NULL) return NULL;
	if (recordID <= 0 || m_numberOfRecords == 1)
		return removeFirstRecord();
	else
	{
		// removing node is neither the first nor the last item
		// get the node before and after the item to be removed
		RecordClass* lpRemovedRecord;
		RecordClassNode* lpPreviousNode = f_getRecordNode(recordID-1);
		if (lpPreviousNode == NULL) return NULL;
		RecordClassNode* lpNode = lpPreviousNode->m_lpNext;
		if (lpNode == NULL) return NULL;
		RecordClassNode* lpNextNode = f_getRecordNode(recordID+1);
		// remove lpNode
		lpPreviousNode->m_lpNext = lpNextNode;
		if (lpNextNode != NULL)
		{
			lpNextNode->m_lpPrevious = lpPreviousNode;
		}
		// reset the node
		lpRemovedRecord = lpNode->m_lpRecord;
		delete lpNode;
		// update count
		m_numberOfRecords--;
		// return the removed node
		return lpRemovedRecord;
	}
}
template <class RecordClass>
RecordClass* CTL_DoublyLinkedList<RecordClass>::removeRecord( RecordClass* lpRemoveRecord )
{
	if (lpRemoveRecord == NULL || m_lpRoot == NULL) return NULL;
	// find the remove record node
	RecordClassNode* lpRemoveNode = m_lpRoot;
	while (lpRemoveNode != NULL)
	{
		if (lpRemoveNode->m_lpRecord != lpRemoveRecord)
			lpRemoveNode = lpRemoveNode->m_lpNext;
		else
			break;
	}
	if (lpRemoveNode == NULL) return NULL;
	// set the next and previous
	RecordClassNode* lpPrevious = lpRemoveNode->m_lpPrevious;
	RecordClassNode* lpNext = lpRemoveNode->m_lpNext;
	if (lpPrevious != NULL)
		lpPrevious->m_lpNext = lpNext;
	else
		m_lpRoot = lpNext;
	if (lpNext != NULL)
		lpNext->m_lpPrevious = lpPrevious;
	// delete the node
	delete lpRemoveNode;
	m_numberOfRecords--;
	return lpRemoveRecord;
}
template <class RecordClass>
RecordClass* CTL_DoublyLinkedList<RecordClass>::removeFirstRecord(void)
{
	if (m_lpRoot != NULL)
	{
		RecordClass* lpRemoveRecord;
		RecordClassNode* lpRemoveNode = m_lpRoot;
		m_lpRoot = m_lpRoot->m_lpNext;
		if (m_lpRoot != NULL)
			m_lpRoot->m_lpPrevious = NULL;
		// reset the node
		lpRemoveRecord = lpRemoveNode->m_lpRecord;
		delete lpRemoveNode;
		m_numberOfRecords--;
		return lpRemoveRecord;
	}
	return NULL;
}
template <class RecordClass>
RecordClass* CTL_DoublyLinkedList<RecordClass>::removeLastRecord(void)
{
	return removeRecord( m_numberOfRecords-1 );
}
template <class RecordClass>
void CTL_DoublyLinkedList<RecordClass>::promoteRecord(RecordClass* lpRecordToPromote)
{
	// if there is only 1 node, or no nodes, do nothing
	if (m_lpRoot == NULL || lpRecordToPromote == NULL || m_numberOfRecords <= 1) return;
	// find this record's node
	RecordClassNode* lpNodeToPromote = m_lpRoot;
	while (lpNodeToPromote != NULL)
	{
		if (lpNodeToPromote->m_lpRecord == lpRecordToPromote)
			break;
		else
			lpNodeToPromote = lpNodeToPromote->m_lpNext;
	}
	if (lpNodeToPromote== NULL) return;
	// if first item, do nothing
	if (lpNodeToPromote->m_lpPrevious == NULL) return;
	// get pointers to the nodes
	RecordClassNode* lpNode			= lpNodeToPromote;
	RecordClassNode* lpPreviousNode	= lpNode->m_lpPrevious;
	RecordClassNode* lpNextNode		= lpNode->m_lpNext;
	// extract item from list
	lpPreviousNode->m_lpNext	= lpNextNode;
	if (lpNextNode != NULL) lpNextNode->m_lpPrevious = lpPreviousNode;
	// insert before the previous node
	lpNode->m_lpPrevious		= lpPreviousNode->m_lpPrevious;
	lpNode->m_lpNext			= lpPreviousNode;
	lpPreviousNode->m_lpPrevious= lpNode;
	if (lpNode->m_lpPrevious != NULL)
		lpNode->m_lpPrevious->m_lpNext = lpNode;
	else
		m_lpRoot = lpNode;
}
template <class RecordClass>
void CTL_DoublyLinkedList<RecordClass>::demoteRecord(RecordClass* lpRecordToDemote)
{
	// if there is only 1 node, or no nodes, do nothing
	if (m_lpRoot == NULL || lpRecordToDemote == NULL || m_numberOfRecords <= 1) return;
	// find this record's node
	RecordClassNode* lpNodeToDemote = m_lpRoot;
	while (lpNodeToDemote != NULL)
	{
		if (lpNodeToDemote->m_lpRecord == lpRecordToDemote)
			break;
		else
			lpNodeToDemote = lpNodeToDemote->m_lpNext;
	}
	if (lpNodeToDemote== NULL) return;
	// if last item, do nothing
	if (lpNodeToDemote->m_lpNext == NULL) return;
	// get pointers to the nodes
	RecordClassNode* lpNode			= lpNodeToDemote;
	RecordClassNode* lpPreviousNode	= lpNode->m_lpPrevious;
	RecordClassNode* lpNextNode		= lpNode->m_lpNext;
	// extract item from list
	lpNextNode->m_lpPrevious = lpPreviousNode;
	if (lpPreviousNode == NULL)
		m_lpRoot = lpNextNode;
	else
		lpPreviousNode->m_lpNext	= lpNextNode;
	// insert after the next node
	lpNode->m_lpPrevious		= lpNextNode;
	lpNode->m_lpNext			= lpNextNode->m_lpNext;
	lpNextNode->m_lpNext = lpNode;
	if (lpNode->m_lpNext != NULL)
		lpNode->m_lpNext->m_lpPrevious = lpNode;
}
#endif

