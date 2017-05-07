function Q = qlearn()
  % create map
  x = 10; y = 10;

  % actions -- up; down; left; right
  A = [-1; 1; -y; y];

  % initial state
  S = 1;

  % reward matrix, utility matrix, and learning variables
  R = zeros(x,y); R(end) = 100; Q = zeros(x*y,size(A,1)); 
  alpha = 0.2; gamma = 0.2; episodes = 1000;

  % position matrix (for viewing)
  POS = zeros(x,y); POS(S) = 1; POS(end)=2;
  [X,Y] = size(POS);
  imagesc(1:X,1:Y,POS);
  drawnow;
  
  function  qvals = action(S)
    % get neighboring elements
    if S>1 & mod(S,y)~=1, up=Q(S,1); else, up=-inf; end
    if S<x*y & mod(S,y)~=0, down=Q(S,2); else, down=-inf; end
    if S-y>=1, left=Q(S,3); else, left=-inf; end
    if S+y<=x*y, right=Q(S,4); else, right=-inf; end
    qvals=[up down left right];
  end
 
  % vector of random starting positions
  r = randi([1 x*y-1],1,episodes);

  for n = 1:episodes
    running = true;
    while running == true
      
      % evaluate and update q matrix
      qvals = action(S);
      m = max(qvals(:));
      idx = find(qvals==m);
      i = idx(randi(size(idx,2)));
      Q(S,i) = Q(S,i)+alpha*(R(S+A(i))+gamma*max(max(action(S+A(i))))-Q(S,i));
      
      % if landed on final square, break and go to next episode
      if S==x*y, 
        running=false; disp('Restart'); 
        break; 
      end
      % update position matrix
      S=S+A(i);
      POS=0*POS; POS(end)=2; POS(S)=1;
      imagesc(1:X,1:Y,POS);
      drawnow;
    end
  
    % reinitialise the position of the agent to a random point on the grid
    S = r(n); POS = 0*POS; POS(S) = 1;
  end
end
