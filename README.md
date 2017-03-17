Component : AnimatedExpandableListView
This document explains how to use the component

Classes to be Copied :
Copy the following classes from component folder

 *      AnimatedExpandableListView
 *	AnimatedExpandableListAdapter
 *	DummyView
 *	ExpandAnimation
 *	GroupInfo

 Note : Current classes are in the package com.avinash.uihelper, these can either be copied to specified package or
 change them as per requirement.

AnimatedExpandableListView : is used for creating ExpandableListView with Expand and Collapse Animations

Usage :

In Layout:

	<com.avinash.uihelper.AnimatedExpandableListView
                android:id="@+id/expandable_lst"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:background="@android:color/white"
                android:choiceMode="singleChoice"
                android:divider="@android:color/transparent"
                android:groupIndicator="@null"
                android:scrollbars="none"
                android:textColor="@android:color/black" />

In Activity/Fragment:

1) Make the Activity / Fragment implement 
	
	* ExpandableListView.OnGroupClickListener
	* ExpandableListView.OnChildClickListener
	* ExpandableListView.OnGroupExpandListener

2) Usage	

	private AnimatedExpandableListView mExpandableListView;
	private ExpandableListAdapter mExpandableListAdapter;
	private int lastExpandedPosition = -1;
	
```
	
	mExpandableListView = (AnimatedExpandableListView) findViewById(R.id.expandable_lst);
	mExpandableListAdapter = new ExpandableListAdapter(this, mGroupList, mChildList);
        mExpandableListView.setAdapter(mExpandableListAdapter);
        mExpandableListView.setOnGroupClickListener(this);
        mExpandableListView.setOnChildClickListener(this);
        mExpandableListView.setOnGroupExpandListener(this);	
```

```

	@Override
    	public boolean onGroupClick(ExpandableListView parent, View v, int groupPosition, long id) {
        if (mExpandableListView.isGroupExpanded(groupPosition)) {
            mExpandableListView.collapseGroupWithAnimation(groupPosition);
        } else {
            mExpandableListView.expandGroupWithAnimation(groupPosition);
        }
        return true;
    	}
```

```

	@Override
    	public boolean onChildClick(ExpandableListView parent, View v, int groupPosition, int childPosition, long id) {
        // handle click based on child position
        return false;
    	}
```

```

	/**
	* This is done in order to close the previously expanded group
	* when clicked on a new group
	*
	*@param groupPosition
	*/
	@Override
    	public void onGroupExpand(int groupPosition) {
        if (lastExpandedPosition != -1
                && groupPosition != lastExpandedPosition) {
            mExpandableListView.collapseGroup(lastExpandedPosition);
        }
        lastExpandedPosition = groupPosition;
    	}
```

3) Adapter

	* Extend your custom adapter with "AnimatedExpandableListAdapter"
	
	* Implement the methods
		
```

		@Override
    		public View getRealChildView(int groupPosition, int childPosition, boolean isLastChild, View convertView, ViewGroup parent) {
        	return null;
		}

    		@Override
		public int getRealChildrenCount(int groupPosition) {
        	return 0;
		}
```








