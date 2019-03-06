Aka tree walking

- [An interactive explanation of quadtrees.](http://jimkang.com/quadtreevis/)
- [Tree traversal — Wikipedia](https://en.wikipedia.org/wiki/Tree_traversal)
- [Breadth-first search — Wikipedia](https://en.wikipedia.org/wiki/Breadth-first_search)
- [sql - What is the most efficient/elegant way to parse a flat table into a tree? - Stack Overflow](https://stackoverflow.com/questions/192220/what-is-the-most-efficient-elegant-way-to-parse-a-flat-table-into-a-tree)
- [A GPU Approach to Path Finding « null program](http://nullprogram.com/blog/2014/06/22/) - [WebGL Shortest Path Solver](http://nullprogram.com/webgl-path-solver/) [skeeto/webgl-path-solver: WebGL shortest path solver](https://github.com/skeeto/webgl-path-solver)
- [Unity Compute Shader Experiments: GPU Pathfinding - YouTube](https://www.youtube.com/watch?v=1OSXWhd3hvI)

To visit a node for a finite tree
 
	/*
	{
		name: "1",
		childNodes: [
			{
				name: "1-1",
				childNodes: [
					{
						name: "1-1-1",
						childNodes: []
					}
				]
			},
			{
				name: "1-2",
				childNodes: []
			}
		]
	},
	{
		name: "2",
		childNodes: []
	}
	*/

Should be easier if node API implement pointers like: childNodes, parentNode, nextSibling, previousSibiling, firstChild, etc.

## Recursive

Call the visitor function itself on all children

Limited by the call stack if no [tail call optimization](https://en.wikipedia.org/wiki/Tail_call)

	function visitNode(node){
		// Do something with the node
		node.chilren.forEach(visiteNode);
	}

## Stack

Depth-first search like traversal

It support only one root node. It's allow to 

Note: `stack` and `indexes` length are not shrinked during loop iteration, because it's not really needed to do so

	// Will gives: "1", "1-1", "1-1-1", "1-2", "2"
	const rootNode = {childNodes:[/*...*/]};
	let deep = 0;// current position in the stack
	let stack = [rootNode];//array of parent nodes
	let indexes = [];// index of the current child in its children list
	// The loop on nodes and their child
	nodes: while(true){
		// visit the node
		let node = stack[deep];
		// do something with the node data or insert, delete children:
		// visitorStart(node, indexes[deep], stack.slice(0, deep - 1), indexes.slice(0, deep - 1));
		
		// if the node has children, go down visit it
		if(node.childNodes.length){
			deep++;
			indexes[deep] = 0;
			stack[deep] = node.childNodes[0];
			// Continue the loop with the first child node
			continue;
		}
		
		// Else go visit the next sibling or the parent sibling if any
		// or the grand parent sibling if any, and so on until reach the root node
		while (true){
			// end of node visitation (and its children)
			let parentDeep = deep - 1;// -1 for the root node
			let parents = deep == 0 ? [] : stack.slice(0, parentDeep);
			let childIndexes = deep == 0 ? [] : indexes.slice(0, parentDeep);
			// visitorEnd(stack[deep], indexes[deep], parents, childIndexes);
		
			// This is the end. The root node don't have siblings
			if(deep === 0){
				break nodes;
			}
			// Continue with the next sibling child
			let siblings = stack[parentDeep].childNodes;
			let nextSiblingIndex = ++indexes[parentDeep];
			// Test if next sibling exist
			if(nextSiblingIndex < siblings.length){
				stack[deep] = siblings[nextSiblingIndex];
				continue nodes;
			}
			
			// Else no next sibling, go up and try again
			deep--;
		}
	}
	
	stack.length = indexes.length = 1;// clean up the stack

## Accumulation

Depth-first search like traversal

Will accumulate in a queue node to visit. In the loop, lastest added nodes are visited first. Support multiple root nodes.

Simple, but require more memory than [Stack](#stack), because in each loop iteration the queue is updated (remove the last element and concat new elements). It's store current nodes (but all nodes of the tree) that waiting for visitation. Ex: root node contains 100 children. Each children contains 100 children, which contains 100 nodes each (total 100^100^100). The queue will contains at max 199 nodes.

**This method can't track in the loop iteration the deep in the tree.**

	let queue = [rootNode1, rootNode2/*...*/].reverse();// nodes queue waiting for visitation
	while(queue.length > 0){
		let node = queue.pop();
		
		// visite the node
		// do something with the node data or insert, delete child
		
		// Node has children
		if(node.childNodes.length){
			nodes = queue.concat(node.childNodes.slice(0).reverse());// reverse child order to be sure the last is the first visited order
			continue;
		}
	}

## Tree search

Aka pathfinding, path finding

Use JPS+ Goal bounding (A* optimized)

- [GDC Vault - JPS+: Over 100x Faster than A*](http://www.gdcvault.com/play/1022094/JPS-Over-100x-Faster-than) - see [The JPS Pathfinding System - 5212](http://www.aaai.org/ocs/index.php/SOCS/SOCS12/paper/download/5396/5212)
- [Pathfinding — Wikipedia](https://en.wikipedia.org/wiki/Pathfinding)
- [Template:Graph search algorithm — Wikipedia](https://en.wikipedia.org/wiki/Template:Graph_search_algorithm)
- [A* search algorithm — Wikipedia](https://en.wikipedia.org/wiki/A*_search_algorithm)
- [Jump point search — Wikipedia](https://en.wikipedia.org/wiki/Jump_point_search) - Jump Point Search (JPS) is an optimization to the A* search algorithm
- [Shortest path problem — Wikipedia](https://en.wikipedia.org/wiki/Shortest_path_problem)
- [Fast Pathfinding via Symmetry Breaking | AiGameDev.com](http://aigamedev.com/open/tutorial/symmetry-in-pathfinding/)
- [Dijkstra's algorithm — Wikipedia](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)
- [Gamasutra: Matt Klingensmith's Blog - Overview of Motion Planning](http://www.gamasutra.com/blogs/MattKlingensmith/20130907/199787/Overview_of_Motion_Planning.php)
- [ActionScript Architect » Blog Archive » A* 3D – No, really, it’s 3D](http://www.actionscriptarchitect.com/2007/07/03/a-3d-no-really-its-3d/) - 3D version of A*
- [Apply A* to real life for once](https://github.com/mplewis/osm-pathfinding)
- [How to Speed Up A* Pathfinding With the Jump Point Search Algorithm](https://gamedevelopment.tutsplus.com/tutorials/how-to-speed-up-a-pathfinding-with-the-jump-point-search-algorithm--gamedev-5818)
- [PathFinding.js](http://qiao.github.io/PathFinding.js/visual/) - Compare A*, IDA*, Breadth-First-Search, Best-First-Search, Dijkstra, Jump Point Search, Orthogonal Jump Point Search and Trace See https://github.com/qiao/PathFinding.js
- [Hierarchical Open Graph](https://github.com/nathansttt/hog2)
- [Graph, a hidden hero – Youpi !](http://barradeau.com/blog/?p=651) - see https://github.com/nicoptere/graph
- [Fast Pathfinding via Symmetry Breaking | Shortest Path](https://harablog.wordpress.com/2011/08/26/fast-pathfinding-via-symmetry-breaking/), [Rectangular Symmetry Reduction | Shortest Path](https://harablog.wordpress.com/2011/09/01/rectangular-symmetry-reduction/) and [Jump Point Search | Shortest Path](https://harablog.wordpress.com/2011/09/07/jump-point-search/)
- [Fast, lightweight and easy-to-use pathfinding library for grid-based games](https://github.com/Yonaba/Jumper) - Lua Jump Point Search implementation
- [The AI Systems of Left 4 Dead - ai_systems_of_l4d_mike_booth.pdf](http://www.valvesoftware.com/publications/2009/ai_systems_of_l4d_mike_booth.pdf) - Use of A* in game. See [The AI Systems of Left 4 Dead — Mike Booth](The AI Systems of Left 4 Dead — Mike Booth.pdf)
- [Shining Rock Software](http://www.shiningrocksoftware.com/2013-04-29-tech-stuff-3-pathfinding/) and [Shining Rock Software](http://www.shiningrocksoftware.com/2013-11-21-more-bugs-pathfinding-problems/) - More Bugs: Pathfinding Problems
- [The StarCraft path-finding hack - Code Of Honor](http://www.codeofhonor.com/blog/the-starcraft-path-finding-hack) - sometimes ignore collisions with moving object (couldn't be noticed)
- [anvaka/ngraph.path: Path finding in a graph](https://github.com/anvaka/ngraph.path)